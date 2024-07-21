---
title: The case for fish
description: Why using the fish shell is not as bad as you think
date: 2024-07-21
---

I've been using the [fish shell](https://fishshell.com/) for a few years now, but whenever I try to convince a friend to switch to it (or even give it a try) - I am met with the same two answers:

- **It's not POSIX compliant, my scripts wouldn't be portable**
- **I don't want to learn a new shell, I'm already comfortable with bash**

And they are right, it's not POSIX compliant - but that's not nearly as important as you might think.

![Fish shell](fish.png "Fish shell")

## POSIX compliance doesn't matter
The only thing your choice of shell affects is one-liners. Using fish doesn't **force** you to write fish scripts (_though they are better_) - you can still write and use bash scripts like you used to.

Consider the ways you'd run a script:
- `./script.sh` (requiring a `#!/bin/bash` shebang at the start)
- `bash script.sh`

Both of them require you to specify a shell, therefore the issue of script portability is not actually real. Using fish would never affect your bash scripts. And do your one-liners really need to be portable? If you're writing a one-liner, it's probably a throwaway command that you'll never use again.

## You don't really need to learn fish
Fish is designed to be user-friendly - and the only differences with bash are ones you'd appreciate. The syntax is infinitely more consistent, intuitive and the documentation is great. A bash/zsh user should be able to learn fish really quickly.

**But you don't actually have to**. The only thing that really changes is the shell you use interactively - and it's a massive improvement.

Sure, you'll need to learn a few concepts, but that will literally take 15 seconds:
- `set` instead of `export`
- `(nothing)/end` instead of `do/done`, `then/fi`, etc.
- `()` for a subshell instead of `$()`, but fish would have told you that if you tried to use `$()` anyway

Oh wait, that's probably all you need to know for basic usage. You can learn the rest as you go - after all, you'll likely need to google the convoluted bash syntax every time you write a script anyway, so might as well google the fish syntax instead.

## Fish is better
Switching to fish would immediately make your shell experience better. You're really sabotaging yourself by being a "purist" and thinking that POSIX compliance is somehow more important than your own convenience.

### Previews
Fish previews commands, filenames and history as you type them.

Like to spam the up arrow key to find the command you ran 5 minutes (or a year) ago? Instead, start by typing the first few characters (or even a substring) and fish will find it. Also it will remember what commands you ran in a directory too, for more relevant suggestions.

### Autocompletion
Fish has incredible autocompletion built-in. I'm so used to it that I spam the tab key whenever I'm using bash and get disappointed when I get a filename suggestion instead of a relevant command flag. Sure, zsh has good autocompletion too - but fish has it by default.

### ~/.bashrc is a mess
Ah yes, the file you've been dumping your configuration, aliases and functions into for years. If you're more organized, you might have split it into multiple files or directories.

However, fish does that by default - and it automatically reloads whatever function you define in `~/.config/fish/functions/` when you change it.

In addition, fish has a `funcsave` command to save a function/alias you just defined, so you don't even have to open your editor.

### Syntax
Let's compare these two one-line loops demonstrating logic you might need in your daily shell usage (without using any external programs):

**bash**
```sh
for i in {1..10}; do if [[ $(($i % 2)) = 1 ]]; then filename=$i.png; echo ${filename%.*}.jpg; fi; done
```

**fish**
```fish
for i in (seq 1 10); if test (math $i % 2) = 1; set filename $i.png; echo (path change-extension .jpg $filename); end; end
```

These two one-liners are equivalent and output this (with some artificial hoops to jump through along the way):
```
1.jpg
3.jpg
5.jpg
7.jpg
9.jpg
```

It's not hard to spot the oddities in the bash example:
- There are multiple ways to open a block (`do/done` and `then/fi` etc.)
- There are multiple kinds of brackets/parentheses involved (`{}`,  `${}`, `[[]]`, `$(())`)
    > By the way, `[` is secretly an executable, while `[[` is a bash keyword - and they're different!
- The math syntax doesn't even imply that math would be happening inside `$((1 + 2))`
- The syntax to strip a file extension looks like dark magic `${filename%.*}`

There is no way to honestly say that the bash example is more readable, easier or "better" in any way.

## I sound like a salesman
Fish isn't perfect, but it's such a massive improvement over bash that I think it outweighs all the downsides many times over.

I'm not saying you should absolutely switch to fish - but I am saying you should give it a try. And I don't mean "use it for a day and then switch back" - I mean actually give it a chance. You might be surprised how much you like it.
