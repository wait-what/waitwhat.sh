---
title: Dark square, no click!
date: 2021-06-10
description: A game inspired by White tile, don't tap it!
project:
    language: rust
    repo: https://github.com/wait-what/dark-square-no-click
    featured: true
---

![Dark square, no click!](https://github.com/wait-what/dark-square-no-click/raw/master/screenshot.png "Dark square, no click!")

A game inspired by White tile, don't tap it!

## Game rules
- There is a 4x4 (customizable) grid with 3 targets (customizable)
- You have 15 seconds (customizable) to click as many white squares as you can
- The game ends when you click a black square or run out of time
- You can use `left`/`right` mouse buttons and `Z`/`X` on your keyboard to click the squares
- To restart, press `space`

## Download
If you want to try it, you can [download it here](https://github.com/wait-what/dark-square-no-click/releases). It runs on **Linux** and **Windows**.

## Macroquad
[Macroquad](https://macroquad.rs/) is a great and simple game library for the [Rust](https://www.rust-lang.org/) programming language. It allows you to create small games very quickly, and it is rather performant.

## Web assembly?
It should be possible to port this to WebAssembly with minimal effort, but I haven't gotten around to it yet. If someone else wishes to do it, feel free to [open a pull request](https://github.com/wait-what/dark-square-no-click)
