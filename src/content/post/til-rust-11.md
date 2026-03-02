---
title: "TIL RUST #11: The @ Operator, Exhaustiveness checking, and Guard Clauses"
description: "The @ Operator, Exhaustiveness checking, and Guard Clauses"
publishDate: "2025-12-20"
tags: ["rust"]
---

## The @ Operator

The `@` operator in Rust allows you to bind a matched value to a variable while simultaneously applying a pattern to it. This means you can both test whether a value matches a specific pattern AND capture that value for use in your code.

Consider this example:

```rust
match age() {
    0 => println!("I haven't celebrated my first birthday yet"),
    // The @ operator binds the matched value to a variable while also matching a pattern
    n @ 1..=12 => println!("I'm a child of age {:?}", n),
    n @ 13..=19 => println!("I'm a teen of age {:?}", n),
    // Catch-all pattern: matches any remaining value and binds it to n
    n => println!("I'm an old person of age {:?}", n),
}
```

Without the `@` operator, you might lose the specific value after matching a range. You could use guard clauses, but they don't contribute to Rust's exhaustiveness checking.

## Exhaustiveness checking

Rust ensures your `match` expressions handle every possible value of the type at compile time. 

```rust
enum UserRole {
    Admin,
    Moderator, 
    Regular,
}
```

If you match on `UserRole` but forget the `Regular` case, the compiler will error out: "pattern UserRole::Regular not covered".

## The Problem with Guard Clauses

Guard clauses don't participate in exhaustiveness checking. 

```rust
match age {
    n if n >= 0 && n <= 12 => println!("Child: {}", n),
    n if n >= 13 && n <= 19 => println!("Teen: {}", n),
    n if n >= 20 => println!("Adult: {}", n),
}
```

The compiler doesn't know the guards cover specific ranges; it only sees variable bindings. Using `@` patterns gives the compiler range information, catching uncovered values at compile time.
