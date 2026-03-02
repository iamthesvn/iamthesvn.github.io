---
title: "TIL RUST #1"
description: "Learning about rustdoc, its significance, and how to use it for API documentation."
publishDate: "2025-11-07"
tags: ["rust"]
---

## `rustdoc`

I hadn't tried using `rustdoc` so far, and I wanted to learn its importance via a simple program, but before that, I wanted to understand its significance. What makes it different from using `//` or `/* */`?

`//` and `/* */` are intended for developers reading the source code, whereas `///` or `//!` are used to generate API documentation.

By using `///` or `//!`, you make it easy to prepare API documentation that is generated via the `rustdoc` command. Pretty cool.

> Note: I actually used `cargo doc --open` as a proxy to use `rustdoc`, as I was just testing this feature and didn't need to use the granular options and flags offered by `rustdoc`.

## Some dumb things I have been doing

One of the dumb things I have been doing so far in my Rust everyday repo is creating a new package with `cargo new examplename` for every new exercise I wanted to create. However, this is not necessary; I could have just created a vanilla Rust file (inside the `src/bin` directory) with the examples and run them.

As an auditor/security researcher, I never paid attention to these things, but I guess a developer is expected to have an organized repo. I plan on reorganizing the repo to correct this mistake.

I can't wait to learn all the other dumb things I have been doing and find the best ways to avoid them in the future. Not gonna lie, I didn't think learning Rust and recording my learnings on 𝕏 would be this exciting.

"Let's get rusty!"
