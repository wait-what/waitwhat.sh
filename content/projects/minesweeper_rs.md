---
title: minesweeper-rs
date: 2021-09-24
description: My implementation of Minesweeper in Rust.
project:
    language: rust
    repo: https://github.com/wait-what/minesweeper-rs
    featured: true
---

![minesweeper-rs](https://github.com/wait-what/minesweeper-rs/raw/master/screenshot.png "minesweeper-rs")

This idea randomly popped into my head for no particular reason. I came up with all the algorithms in a few seconds, mostly by accident, and I was able to implement them in rust.

## Download
If you want to try it, you can [download it here](https://github.com/wait-what/minesweeper-rs/releases). It runs on **Linux** and **Windows**.

## Features
- Adjustable width and height
- Adjustable mine count (using percentage)
- Adjustable colours
- Timer
- Area highlighting when right-clicking number
- Automatic restarts until a 0 cell is clicked

## Controls
- Left click to reveal cell
- Right click unexplored area to place a flag
- Right click a number to highlight the area it belongs to
- Space to open settings
- R to restart

## Macroquad
[Macroquad](https://macroquad.rs/) is a great and simple game library for the [Rust](https://www.rust-lang.org/) programming language. It allows you to create small games very quickly, and it is rather performant.

## Web assembly?
It should be possible to port this to WebAssembly with minimal effort, but I haven't gotten around to it yet. If someone else wishes to do it, feel free to [open a pull request](https://github.com/wait-what/minesweeper-rs)
