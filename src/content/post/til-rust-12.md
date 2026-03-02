---
title: "TIL RUST #12: if let Pattern Matching and debug_assert!"
description: "if let Pattern Matching and debug_assert!"
publishDate: "2025-12-21"
tags: ["rust"]
---

## `if let` Pattern Matching

`if let` statements provide a concise way to pattern match on enums and extract values, especially useful for `Option` types. They combine conditional checking with destructuring in a single expression.

```rust
fn main(){
    let number = Some(7);

    // if let destructures Option and binds the inner value
    if let Some(i) = number {
        println!("Matched {:?}!", i);
    }
}
```

- `if let Some(i) = number` destructures `Option` types. When `number` is `Some(7)`, the pattern `Some(i)` matches and binds `7` to `i`.
- Unlike full `match` statements, `if let` only handles the cases you specify, making it ideal for concise `Option` handling.

## The `debug_assert!` macro

Unlike in C++, Rust's `assert!` macro is always checked. However, we can use the `debug_assert!` macro for assertions that are skipped in optimized builds.

- Use `assert!` for uncompromisable safety nets (e.g., bounds in unsafe blocks).
- Opt for `debug_assert!` for developer-time validations.
