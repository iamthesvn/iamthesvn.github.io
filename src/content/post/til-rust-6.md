---
title: "TIL RUST #6: Difference between a library and an executable"
description: "Difference between a library and an executable"
publishDate: "2025-11-12"
tags: ["rust"]
---

## Difference between a library and an executable

A library crate provides functionality or reusable code intended to be used by other crates. It does **not** have a main() function and does not compile to a standalone executable.

An executable crate compiles to a runnable program with an entry point fn main(). It produces a standalone binary that can be run directly by the operating system. Executables often depend on one or more libraries.
