---
title: "TIL RUST #12"
description: "if let Pattern Matching and debug_assert!"
publishDate: "2025-12-21"
tags: ["rust", "til", "if-let", "macros", "debugging"]
---

## `if let` Pattern Matching

`if let` statements provide a concise way to pattern match on enums and extract values, especially useful for `Option` types. They combine conditional checking with destructuring.

Example (from Rust by Example: [https://doc.rust-lang.org/rust-by-example/flow_control/if_let.html](https://doc.rust-lang.org/rust-by-example/flow_control/if_let.html)):

```rust
fn main() {
    let number = Some(7);
    if let Some(i) = number {
        println!("Matched {:?}!", i);
    }
}
```

Unlike full `match` statements that require handling all cases exhaustively, `if let` is ideal for single-case logic.

## The `debug_assert!` macro

`assert!` is always checked. `debug_assert!` is skipped in optimized builds, making it perfect for dev-time validations without production overhead.
