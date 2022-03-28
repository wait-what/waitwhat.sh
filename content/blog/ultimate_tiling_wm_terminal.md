---
title: Ultimate tiling wm terminal
description: The best terminal experience on a tiling wm on arch (imo) using alacritty and fish
date: 2021-11-02
---

So, you're using a [tiling window manager](https://en.wikipedia.org/wiki/Tiling_window_manager) and want to rice your terminal? Well, I've done all the hard work for you.

> This guide is mostly targeted at Arch linux users

![Result](alacritty.png "Result")

## Installation
First of all, you will need to install some packages. Some of those packages are from [AUR](https://wiki.archlinux.org/title/Arch_User_Repository) so it would be useful to have an [AUR helper](https://wiki.archlinux.org/title/AUR_helpers) like [paru](https://github.com/morganamilo/paru) or [yay](https://github.com/Jguer/yay) installed.

- The terminal itself: `alacritty`
- The best shell of all: `fish`
- Cool looking things: `neofetch` and `pfetch`
- Fonts: `ttf-fira-code`
- A theme picker for alacritty: `alacritty-themes`
- Lolcat to make text rainbow: `lolcat`

If you have paru, you can just run this command to install all the packages:

```sh
paru -Syu alacritty alacritty-themes ttf-fira-code fish neofetch pfetch lolcat
```

## Configuring alacritty
After opening alacritty, open it's configuration file located in `~/.config/alacritty/alacritty.yml`.

Here is my recommended configuration to get started with:
```yaml
font:
  size: 12
  normal:
    family: Fira Code
  bold:
    family: Fira Code
  italic:
    family: Fira Code
env:
  TERM: xterm-256color
```

> You will likely need to adjust `font.size` to match your preference!

The next step is to set a theme. Here is a cool trick: run `neofetch` before running `alacritty-themes` to have some example text to judge the themes.

So, in a nutshell:

```sh
neofetch && alacritty-themes
```

Press arrow up and down until you find a theme you like. Then press enter.

## Configuring fish
### Setting the default shell
First of all, you need to set fish as your default shell.

```sh
chsh -s /usr/bin/fish
```

And then enter fish by either restarting alacritty or simply running `fish`.

### Oh my fish!
Now that you have fish as your default shell, you can install `oh-my-fish`. It is a theme manager for fish and you can use it to install themes very easily.

Simply running this command should do the trick:

```sh
curl -L https://get.oh-my.fish | fish
```

Now you'll need to pick out a theme you like from [this list of `oh-my-fish` themes](https://github.com/oh-my-fish/oh-my-fish/blob/master/docs/Themes.md)

Then install the theme using `omf install <theme name>`.

So for example, if you like `boxfish` run this:

```sh
omf install boxfish
```

### Setting a fish greeting
The `fish_greeting` function runs every time you open a new terminal, kind-of like `~/.bashrc`

We're going to make it run `pfetch` every time you open fish, and pass it into `lolcat` to make it rainbow.

```fish
function fish_greeting
  echo
  pfetch | lolcat
end

funcsave fish_greeting
```

## Congratulations
You did it! See the results by restarting alacritty.
