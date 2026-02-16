---
title: "TIL RUST #2: Running the main source file of a package and other files in src/bin"
description: "Running the main source file of a package and other files in src/bin"
publishDate: "2025-11-08"
tags: ["rust", "til", "cargo", "learning"]
---

## Running the main source file of a package and other files in src/bin

You should be somewhere inside your package's directory, which contains the Cargo.toml file, in order to run the package with Cargo. You do not need to be in the root itself; any subdirectory will work.

The same applies even to other source files (in src/bin), but a flag (`--bin`) must be used in conjunction with the regular `cargo run` command.

Example:
```shell
cargo run --bin <nameofbinary>
```

## cargo clean

This CLI command cleans up all the executables compiled from the source code files and placed in the targets subdirectory. This ensures a fresh build and also helps free up disk space.

## Four-space indentation

Four-space indentation is standard Rust style. Running `rustfmt` on your source code file defaults to this indentation style. 

Richard wouldn't be happy! 

Context:
https://youtu.be/cowtgmZuai0?si=QnTQtmF4zqVZULjX

## Semicolon and statements

Adding a semicolon after an expression turns it into a statement, so nothing is returned; without the semicolon, the value is returned.

Functions (with no return statements) that expect a specific return type that is not the unit type might run into compilation errors when you end the function with a semicolon.

## Test functions

These functions are ignored when you execute `cargo build` or `cargo run`. To run the test functions, the `cargo test` command is used.

Each test function is annotated with the `#[test]` attribute. Also, `#[cfg(test)]` is used when the test functions are written in the source code files.
