---
title: "TIL RUST #11"
description: "The @ Operator, Exhaustiveness checking, and Guard Clauses"
publishDate: "2025-12-19"
tags: ["rust", "til", "match", "patterns", "flow-control"]
---

## The @ Operator

The `@` operator in Rust allows you to bind a matched value to a variable while simultaneously applying a pattern to it.

```rust
match age() {
    0 => println!("I haven't celebrated my first birthday yet"),
    n @ 1..=12 => println!("I'm a child of age {:?}", n),
    n @ 13..=19 => println!("I'm a teen of age {:?}", n),
    n => println!("I'm an old person of age {:?}", n),
}
```

*(Link to complete example: [https://doc.rust-lang.org/rust-by-example/flow_control/match/binding.html](https://doc.rust-lang.org/rust-by-example/flow_control/match/binding.html))*

## Exhaustiveness checking

Rust ensures your match expressions handle every possible value of the type. The compiler will reject code if patterns aren't covered.

## The Problem with Guard Clauses

Guard clauses don't participate in exhaustiveness checking. The compiler cannot use guard conditions for coverage verification. Using `@` patterns provides range information that the compiler can rely on for safety.
