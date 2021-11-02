---
title: rust-grid
date: 2021-09-24
description: Very minimal rust library to store large grids of any type in memory, with a user-friendly interface
project:
    language: rust
    repo: https://github.com/wait-what/rust-grid
    featured: false
---


rust-grid is a very minimal library to store large grids of any type in memory, with a user-friendly interface.

## Why?
I was trying to implement [Game of life](https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life) in rust, and I needed a way to store the grid in memory. I made a huge grid and it overflowed the stack, so I made a cool library to store it in a 2D Vec.

I later found out that [better ones](https://crates.io/crates/grid) already exist, but it was too late. At least I made and [published a crate](https://crates.io/crates/rust-grid) - it was fun.

## Example
```rs
use rust_grid::*;

fn main() {
    let grid: Grid<bool> = Grid::new(10, 15, false);

    // Two ways to access data
    let (x, y) = (3, 4);
    println!("{}", grid[y][x]);
    println!("{}", grid[(x, y)]);

    // Get the size
    let (width, height) = grid.size();
}
```
