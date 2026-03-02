---
title: "TIL RUST #4: Scalar and Compound types"
description: "Scalar and Compound types in Rust"
publishDate: "2025-11-10"
tags: ["rust"]
---

## Scalar and Compound types

In Rust, types are classified as scalar or compound based on whether they represent a single value or a collection of values. Scalar types represent single values:
- signed integers
- unsigned integers
- floating point
- char
- bool
- unit type

Note: Although the value of the unit type is a tuple, it is not considered a compound type as it does not contain multiple values.

Compound types represent a collection of values:
- tuples
- arrays
- slices
- structs
- enums

## Suffix annotation

In Rust, numbers can also be annotated with their type through suffix annotation.

Example:
```rust
//normal type annotation
let a: i64 = 23

//suffix annotation
let a = 23i64
```

Also, unless explicitly mentioned, integers default to `i32` and floats to `f64`.

## The Rust compiler modes

`rustc` itself does the frontend and mid-end of compilation, producing the MIR (Mid-level Intermediate Representation), and then lowers MIR to LLVM-IR. From there, the LLVM backend takes the LLVM-IR and compiles it down to machine code for the target architecture.

## Additional (not so important) note

Underscores can be inserted in numeric literals to improve readability, e.g. `1_000` is the same as `1000`, and `0.000_001` is the same as `0.000001`.
