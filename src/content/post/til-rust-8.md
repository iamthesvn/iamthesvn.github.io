---
title: "TIL RUST #8"
description: "Closures in Rust"
publishDate: "2025-11-14"
tags: ["rust", "til", "closures", "learning"]
coverImage:
  src: "https://pbs.twimg.com/media/G5s2NmCbgAAco4-?format=jpg&name=medium"
  alt: "TIL RUST #8 Image"
---

![Cover](https://pbs.twimg.com/media/G5s2NmCbgAAco4-?format=jpg&name=medium)

## Closures in Rust

Closures in Rust are anonymous functions that can capture values from their surrounding environment. Unlike regular functions, closures use **`||`** around input variables, with input names required but types usually inferred. 

They can have single-line bodies without braces or multi-line bodies wrapped in **`{}`**.

Closures are anonymous, assigned to variables, and can be called like functions. I'll demonstrate the primary differences between closures and regular functions through the following example:

```rust
fn main() {
    let greeting = "Hello";
    let greet = |name: &str| format!("{}, {}!", greeting, name);

    println!("{}", greet("Alice")); // Prints: Hello, Alice!
    
    let no_args = || 100;
    println!("Closure returns: {}", no_args());
}

```

In this example, the closure `greet` captures the surrounding variable `greeting` and uses it to create a personalized message. It takes one input parameter, `name`, and returns a formatted string. The closure `no_args` takes no parameters and returns 100. 

Both closures use **`||`** to enclose parameters, different from regular functions, which use **`()`**.

Unlike regular functions, which can only access context passed explicitly as parameters, closures automatically capture and use the necessary variables from their scope. This simplifies code that relies on local context.
