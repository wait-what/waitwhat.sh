---
title: ip_dehash
date: 2021-09-24
description: Demonstrate how easy it is to get an IPv4 from it's MD5 hash using brute force
project:
    language: rust
    repo: https://github.com/wait-what/ip-dehash
    featured: false
---

This program exists to demonstrate how trivially easy it is to get an IPv4 from it's md5 hash using the least efficient method: brute force.

Since this program exists purely for educational purposes, it only supports 1 format for the hashed IP: the hash of 4 bytes representing an IPv4.
This could easily be "improved" to add support for other formats.

## Usage
1. Download the program from [releases](https://github.com/wait-what/ip-dehash/releases) or compile it yourself
1. Input the hash. For example, you could use `a54f0041a9e15b050f25c463f1db7449` for benchmarking. This is the hash of the IP `255.255.255.255`, so, the one that would take the longest.
1. The results will be printed to the terminal
