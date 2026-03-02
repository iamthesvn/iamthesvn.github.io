---
title: "TIL RUST #10: Understanding references, mutability, and pattern matching"
description: "Understanding references, mutability, and pattern matching"
publishDate: "2025-12-16"
tags: ["rust"]
---

Understanding references and mutability is crucial when pattern matching in Rust. For some context, I took the following notes while practicing this example: https://doc.rust-lang.org/rust-by-example/flow_control/match/destructuring/destructure_pointers.html

The following is the code snippet from the example:

```rust
fn main() {
    // Assign a reference of type `i32`. The `&` signifies there
    // is a reference being assigned.
    let reference = &4;

    match reference {
        // If `reference` is pattern matched against `&val`, it results
        // in a comparison like:
        // `&i32`
        // `&val`
        // ^ We see that if the matching `&`s are dropped, then the `i32`
        // should be assigned to `val`.
        &val => println!("Got a value via destructuring: {:?}", val),
    }

    // To avoid the `&`, you dereference before matching.
    match *reference {
        val => println!("Got a value via dereferencing: {:?}", val),
    }

    // What if you don't start with a reference? `reference` was a `&` 
    // because the right side was already a reference. This is not
    // a reference because the right side is not one.
    let _not_a_reference = 3;

    // Rust provides `ref` for exactly this purpose. It modifies the
    // assignment so that a reference is created for the element; this
    // reference is assigned.
    let ref _is_a_reference = 3;

    // Accordingly, by defining 2 values without references, references
    // can be retrieved via `ref` and `ref mut`.
    let value = 5;
    let mut mut_value = 6;

    // Use `ref` keyword to create a reference.
    match value {
        ref r => println!("Got a reference to a value: {:?}", r),
    }

    // Use `ref mut` similarly.
    match mut_value {
        ref mut m => {
            // Got a reference. Gotta dereference it before we can
            // add anything to it.
            *m += 10;
            println!("We added 10. `mut_value`: {:?}", m);
        },
    }
}
```

## Reference Creation

`let reference = &4` creates an immutable borrow, enabling zero-cost abstractions without ownership transfer. This is fundamental to Rust's memory safety model.

## The `mut` Keyword

- **In Variable Bindings**: `let mut mut_value = 6` makes the binding mutable, allowing reassignment or modification. Without `mut`, variables are immutable by default.
- **In Pattern Matching**: `ref mut m` creates a mutable reference to matched values, enabling in-place modifications.

## The `ref` Keyword

- **In Variable Bindings (Rare)**: `let ref _is_a_reference = 3` creates a reference instead of moving/copying. Equivalent to `let _is_a_reference = &3`.
- **In Pattern Matching (Common)**: `ref r` borrows matched values instead of moving them, creating references without taking ownership.

**Key Differences:**

```rust
let _not_a_reference = 3;     // Regular binding - moves/copies
let ref _is_a_reference = 3;  // Reference binding - borrows
let value = 5;                // Immutable binding  
let mut mut_value = 6;        // Mutable binding
```

## Output Formatting

While `println!("{}", val)` and `println!("{:?}", val)` might seem similar, they are quite different:
- `{}` uses the `Display` trait for user-friendly output.
- `{:?}` uses `Debug` for detailed debugging information (often showing quotes or field names).
