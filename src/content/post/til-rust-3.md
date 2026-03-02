---
title: "TIL RUST #3: The Rust compiler converts source code into IR"
description: "The Rust compiler converts source code into IR"
publishDate: "2025-11-10"
tags: ["rust"]
---

## The Rust compiler converts source code into IR

I had always thought that the Rust compiler compiled the source code directly into machine code. But that is not the case. The Rust compiler converts it into an Intermediate Representation (IR), which is then converted into machine code.

More on this here: https://rustc-dev-guide.rust-lang.org/overview.html

## Borrow checker

Rust does not have a garbage collector. Instead, it depends on the borrow checker to ensure memory safety. The borrow checker is very detailed and needs a whole article by itself, so I am saving this for another day.

## Panics in HashMap

In Rust, accessing an element that does not exist in a HashMap using the `get` method does not cause a panic. Instead, `get` returns an `Option<&V>`, which is `None` if the key is not found, or `Some(&value)` if it is. 

However, if you try to access a value from a HashMap using the indexing syntax `map[&key]` and the key is missing, Rust will panic at runtime. This is similar to accessing an out-of-bounds index in an array.

## Dead code analyzer

This is a lint feature in `rustc` (Rust compiler) that detects unused code elements that are not exported and never used within a crate. This helps devs improve code clarity and maintainability.

Note: Although the dead code analyzer is part of `rustc`, the dead code is treated as a warning by default, not as a compilation error. Developers can also suppress these warnings with attributes like `#[allow(dead_code)]`.
