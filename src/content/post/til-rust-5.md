---
title: "TIL RUST #5: Vectors, Traits, Invocation of rustc, and Lexing"
description: "Vectors, Traits, Invocation of rustc, and Lexing"
publishDate: "2025-11-11"
tags: ["rust"]
---

## Vectors

Vectors in Rust are essentially Rust's dynamic, growable version of arrays. While arrays in Rust are fixed-size collections determined at compile time and are typically stored on the stack, vectors can resize dynamically at runtime and store their data on the heap.

## Traits

Traits define the set of methods that can be called on a type. They are similar to interfaces in other languages.

Example:
```rust
pub trait Summary {
    fn summarize(&self) -> String;
}
```

The above is an example of a trait. It defines a trait called summary, which contains the method `summarize`. When defining a trait, we don't write the implementation of the method; that is left to the types that implement this trait.

The following is an example of two structs implementing the above trait `Summary`:

```rust
pub struct NewsArticle {
    pub headline: String,
    pub location: String,
    pub author: String,
    pub content: String,
}

impl Summary for NewsArticle {
    fn summarize(&self) -> String {
        format!("{}, by {} ({})", self.headline, self.author, self.location)
    }
}

pub struct SocialPost {
    pub username: String,
    pub content: String,
    pub reply: bool,
    pub repost: bool,
}

impl Summary for SocialPost {
    fn summarize(&self) -> String {
        format!("{}: {}", self.username, self.content)
    }
}
```

The example was taken from here: https://doc.rust-lang.org/book/ch10-02-traits.html

## Invocation of rustc

The work that the compiler needs to perform is defined by command-line options. The commands given in the CLI that are targeted towards `rustc` are parsed in `rustc_driver`. This crate contains the definitions of all the compilation configurations/options that can be requested by the user. 

## Lexing

The Rust source that we provide to the compiler is first analyzed by the low-level lexer present in `rustc_lexer`. The lexer converts this source code into the smallest possible individual pieces of source code that have independent meaning for further processing. These units are called tokens.

`rustc` then does parsing, AST lowering, MIR lowering, and Code generation, which I will cover in the upcoming articles.
