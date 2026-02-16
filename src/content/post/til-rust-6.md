---
title: "TIL RUST #6"
description: "Libraries vs Executables, Modules vs Crates, and #[macro_use]"
publishDate: "2025-11-12"
tags: ["rust", "til", "crates", "modules", "macros"]
coverImage:
  src: "https://pbs.twimg.com/media/G5kcQCEbgAALSRi?format=jpg&name=medium"
  alt: "TIL RUST #6 Image"
---

![Cover](https://pbs.twimg.com/media/G5kcQCEbgAALSRi?format=jpg&name=medium)

## Difference between a library and an executable

A library crate provides functionality or reusable code intended to be used by other crates. It does **not** have a main() function and does not compile to a standalone executable.

An executable crate compiles to a runnable program with an entry point fn main(). It produces a standalone binary that can be run directly by the operating system. Executables often depend on one or more libraries.

## Difference between a module and a crate

In Rust, a crate and a module are both ways to organize code, but they operate at different levels of granularity and serve distinct purposes.

A **crate** is the smallest compilation and linking unit in Rust. It can be a binary (executable) or a library. A crate is essentially a whole project or package that can be compiled independently.

A **module** is a way to organize code within a crate. It is like a folder or namespace inside the crate. Modules allow you to group related functions, structs, traits, and other items logically. Modules form a tree structure rooted at the crate root module.

## #[macro_use]

The #[macro_use] attribute in Rust serves mainly to import macros from other modules or external crates in a way that brings these macros into scope for the current module or crate.

When applied to a **module**, it extends the scope of macros defined inside that module so they can be used outside the module without explicit imports.

When applied to an **external crate** (with extern crate), it imports the macros defined in that crate into the current crate's namespace, making them globally available without needing to explicitly bring each macro into scope with use.
