---
title: "TIL RUST #7: Understanding String vs &str in Rust"
description: "Understanding String vs &str in Rust"
publishDate: "2025-11-13"
tags: ["rust"]
---

## Understanding `String` vs `&str` in Rust

Consider this example:

```rust
#[derive(Debug)]
struct Person {
    name: String,
    age: u8,
}
fn main() {
    let name = String::from("Peter");
    let age = 27;
    let peter = Person { name, age };
    println!("{:?}", peter);
}
```

Specifically, this line:
```rust
let name = String::from("Peter");
```
Why should we do this? Why not the following?
```rust
let name = "Peter"
```
To understand why this fails, let’s quickly recap ownership and borrowing in Rust.

## Ownership and Borrowing
Rust's ownership system ensures memory safety without a garbage collector:
- **Ownership**: Each value has one owner. When the owner goes out of scope, the value is cleaned up.
- **Borrowing**: You can reference data without owning it using & (immutable) or &mut (mutable).

Note: "Peter" is borrowed data (&str), but our struct needs owned data (String). Rust requires explicit conversion because ownership affects how memory is managed.

With ownership in mind, let's look closer at Rust's two main string types.

## Two String Types
Rust has two main string types:

1. `&str` (String Slice)
- A borrowed reference to string data.
- Immutable.
- Points to data stored elsewhere (e.g., in the binary or owned by a `String`).
- No allocation needed.

Example:
```rust
let greeting = "Hello";  // This is &str
```

2. `String` (Owned String)
- An owned, growable string.
- Mutable (can be modified).
- Heap-allocated.
- You own it and can move or drop it.

Example:
```rust
let greeting = String::from("Hello");  // This is String
```

## The Type Mismatch Problem
When we defined the struct:
```rust
struct Person {
    name: String,  // This field expects an owned String
    age: u8,
}
```
The name field is String, not &str. So:
```rust
let name = "Peter";  // This is &str
let peter = Person { name, age };  // This causes type mismatch
```
Rust won't automatically convert &str to String here.
And hence, we need to do an explicit conversion:
```rust
let name = String::from("Peter");  // Convert &str to String
let peter = Person { name, age };  // This works
```

Now, I know what you’re thinking: why not define the struct so the name field is of type &str? You’re absolutely right, this is possible. However, doing so introduces the concept of lifetimes, which isn’t crucial for the current example. We’ll save lifetimes for another day.

## Mutation
Mutation refers to changing the value of a variable after it’s been declared. Rust variables are immutable by default; we use `mut` keyword to allow mutation.
```rust
fn main() {
    let mut number = 5;
    number = 3; 
    println!("Number plus two is: {}", number + 2);
}
//Output: Number plus two is: 5
```
Mutation lets us change a variable’s value, but sometimes we need to change its type. That’s where shadowing comes in.

## Shadowing
Shadowing happens when you declare a new variable with the same name as a previous one in the same scope. The original variable is “shadowed” and inaccessible, replaced by the new value and possibly the new type.
```rust
fn main() {
    let number = "T-H-R-E-E"; 
    println!("Spell a number: {number}");

    let number = 3; //the previous "number" variable gets shadowed here
    println!("Number plus two is: {}", number + 2);
}
//Output:
//Spell a number: T-H-R-E-E
//Number plus two is: 5
```

## Constants require an explicit type annotation
In Rust, unless explicitly type-annotated, integer literals default to i32 and floating point literals default to f64.
However, constants need to be type-annotated; if no type is specified, the compiler would flag an error.
```rust
const NUMBER = 3;
fn main() {
    println!("Number: {NUMBER}");
}
```
The above code will run into a compile error; the following, however, would work smoothly and print the output "Number: 3" :
```rust
const NUMBER: i32 = 3;
fn main() {
    println!("Number: {NUMBER}");
}
//Output:
//Number: 3
```
