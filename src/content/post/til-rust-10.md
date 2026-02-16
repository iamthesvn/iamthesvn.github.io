---
title: "TIL RUST #10"
description: "Destructuring pointers, mut keyword, and ref keyword"
publishDate: "2025-12-16"
tags: ["rust", "til", "patterns", "references", "mutability"]
---

*Understanding references and mutability is crucial when pattern matching in Rust. For some context, I took the following notes while practicing this example:*

[https://doc.rust-lang.org/rust-by-example/flow_control/match/destructuring/destructure_pointers.html](https://doc.rust-lang.org/rust-by-example/flow_control/match/destructuring/destructure_pointers.html)

*The following is the code snippet from the example:*

```rust
fn main() {
    let reference = &4;
    match reference {
        &val => println!("Got a value via destructuring: {:?}", val),
    }
    match *reference {
        val => println!("Got a value via dereferencing: {:?}", val),
    }
    let _not_a_reference = 3;
    let ref _is_a_reference = 3;
    let value = 5;
    let mut mut_value = 6;
    match value {
        ref r => println!("Got a reference to a value: {:?}", r),
    }
    match mut_value {
        ref mut m => {
            *m += 10;
            println!("We added 10. `mut_value`: {:?}", m);
        },
    }
}
```

## **Reference Creation**:

`let reference = &4` creates an immutable borrow. This is fundamental to Rust's memory safety model.

## **The mut Keyword**

**In Variable Bindings**: `let mut mut_value = 6` makes the binding mutable. Without `mut`, variables are immutable by default.

**In Pattern Matching**: `ref mut m` creates a mutable reference to matched values.

## **The ref Keyword**

**In Pattern Matching (Common)**: `ref r` borrows matched values instead of moving them, creating references without taking ownership.

**Key Differences**:

```rust
let _not_a_reference = 3;     // Regular binding - moves/copies
let ref _is_a_reference = 3;  // Reference binding - borrows
```

## **Output Formatting**

`{}` uses the `Display` trait for user-friendly output, while `{:?}` uses `Debug` for detailed structural details. `Debug` can be derived using `#[derive(Debug)]`.
