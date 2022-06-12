---
title: Tor secret service under Docker
description: A very simple guide for running a tor hidden service under docker
date: 2022-02-16
---

So, you're running a service (for example, a website) using Docker and you want it to also be available as an `.onion` service on [tor](https://www.torproject.org/), perhaps to improve the anonymity of your users or for fun. I went through all the pain of figuring it out for you.

![Tor logo](tor_logo.jpg "Tor logo")

## Tor domains

On the tor network, you can't register domains like on the clearnet. You own a domain by being in posession of it's private key, which you need to generate yourself.

`.onion` v3 domains are always 56 characters long and are a **random string**, so the only way to get the name you want is by guessing a few million times. Because of the insane amount of guessing involved, you only get a domain that **starts with** 6-7 of the characters you want in a reasonable amount of time. 6 characters usually takes a few minutes to guess, while 7 characters can even take _a few hours_, depending on the hardware.

For example, with `test` as your desired prefix, expect to get domains that look like these:

```
test3u44hhety5osric3tskhcc5m23g2pbz4qecy6i5zqcuhau2ccpad.onion
testatg4gvrp7b7itik7ohxlqidudfbtdzabxodpuafptuyyy6juwtqd.onion
testb5c5ehq2iu5lnzcql2sjnslhhrjmn3na6u2urh3ms2dr7qolbnad.onion
```

## Generating a private key

[mkp224o](https://github.com/cathugger/mkp224o) is a tool that lets you accomplish just that.

You will need basic build tools installed (`build-essential` on debian-based systems, `base-devel` on arch-based systems).

- First, clone the repository

```sh
git clone https://github.com/cathugger/mkp224o
cd mkp224o
```

- Then generate the configuration script

```
./autogen.sh
```

- Then generate the Makefile

```sh
./configure # on intel systems
./configure --enable-amd64-51-30k # on amd systems
```

- You're ready to build the tool

```sh
make
```

- You can now use the tool to generate a private key

```sh
mkdir keys
./mkp224o -B -d keys <prefix>
```

The longer your prefix, the longer it will take. 5 characters is really fast, 6 characters might take a few minutes, and 7 characters might take a few hours or days, depending on your luck.

Once it spits out an .onion domain at you, it's yours! You can stop the generation using `Ctrl+C`. Now go into the `keys` directory and copy the `hs_ed25519_secret_key` to your server.

> Do not share this file, as it's the only thing that makes the domain yours.

## Docker configuration

First, create a directory called `tor` in the same directory where your `docker-compose.yaml` is located.

Now, put the `hs_ed25519_secret_key` in it.

You can just blindly copy this into a file called `Dockerfile` inside the `tor` directory you just created:

> This `Dockerfile` is based on [bariskisir's](https://github.com/bariskisir/HiddenServiceReverseProxy) creation, that unfortunately, did not work for me properly.

```Dockerfile
FROM alpine:latest
RUN apk update && apk add tor
CMD [ "sh", "-c", "echo HiddenServiceDir /tor/service > /tor/config && echo HiddenServicePort $SERVICE >> /tor/config && tor -f /tor/config" ]
```

At this point, your directory structure should look like this:

```
├── docker-compose.yaml
└── tor
    ├── Dockerfile
    └── hs_ed25519_secret_key
```

Lock down the permissions for the tor directory, else tor will refuse to work.

```sh
chmod 400 tor tor/hs_ed25519_secret_key
```

Now add the `tor` service to your `docker-compose.yaml` file.

```yaml
version: "3"

services:
  # Imagine this is the service you're already running
  web:
    image: androw/uhttpd
    volumes:
      - ./www:/www
    # if you only wish it to be accessible via tor, this is optional
    ports:
      - 80:80

  tor:
    build: tor/
    links:
      - web
    environment:
        # 80 is the port on the .onion
        # web:80 is port on the container above
        SERVICE: 80 web:80
    volumes:
      - ./tor:/tor/service
```

Now just `docker-compose up -d` to refresh your configuration and you're done!

## Congratulations!

Now open tor and try to access your new hidden `.onion` service on the _dark web_.

## Troubleshooting

If it isn't working, the first step would be to look at logs of the tor comtainer.

```sh
docker-compose logs -f tor
```

You should also check if your original service itself is still working.
