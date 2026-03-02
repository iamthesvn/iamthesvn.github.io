---
title: "TIL RUST #9: stdout vs stderr, Decoding the Panic, and Stack vs Heap"
description: "stdout vs stderr, Decoding Panic, and Stack vs Heap"
publishDate: "2025-12-01"
tags: ["rust"]
---

## `stdout` vs `stderr` 

At first glance, `println!` and `eprintln!` seem identical. They both output text to the terminal. But separating them unlocks powerful CLI behaviors.

- `stdout` (`println!`) is for your program's actual output.
- `stderr` (`eprintln!`) is for errors and logs.

The cool part is redirection. If I run `cargo run > output.txt`, my normal output saves to the file, but errors still pop up on my screen.

Also, be careful with `>` versus `>>`. A single `>` overwrites the file every time you run it. If you want to keep a log of previous runs, use `>>` to append the new output to the end of the file instead.

## Decoding the Panic

When my code crashed with a panic, I learned that running `RUST_BACKTRACE=1` reveals the "stack trace".

`cargo run with RUST_BACKTRACE=1`

If you use `full` backtrace, you'll even see hex addresses (like `0x1049...`). These point to the Text Segment where your binary's instructions live, which is separate from the stack and heap.

`cargo run with RUST_BACKTRACE=full`

## The Stack vs. Heap

Speaking of memory, I learned a fascinating detail about layout: the Stack and Heap grow towards each other.

- The Stack starts at high memory addresses and grows downward.
- The Heap starts low and grows upward.

They do this to maximize the available free space in the middle without colliding with each other.

## Using `println!` without import

I noticed I never have to import `println!`, but I do have to `use std::io` for input. That's because print commands are macros built into the language, available globally. Input functions like `stdin()` live in the `std::io` module, so you either call them as `std::io::stdin()` or bring them into scope with `use`.
