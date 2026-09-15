---
title: Functions in Rust
---

# Functions in Rust

Functions divide a program into named, reusable units of behavior. Every Rust executable begins with the `main` function, but larger programs become easier to understand when separate tasks have separate functions. A good function usually has one clear responsibility, such as calculating a score, validating input, or displaying a result.

## Parameters and Return Values

Function parameters require explicit types. This gives the compiler enough information to check every call and makes the function's expectations clear to readers.

```rust
fn hand_total(first_card: u8, second_card: u8) -> u8 {
    first_card + second_card
}

fn main() {
    let total = hand_total(10, 7);
    println!("Hand total: {total}");
}
```

The arrow in `-> u8` declares the return type. The final line of `hand_total` has no semicolon because it is an expression whose value is returned. Adding a semicolon would turn it into a statement and discard the value. Rust also supports the `return` keyword, which is particularly useful for leaving a function early, although the final-expression style is common for ordinary results.

## Designing Useful Functions

Breaking a problem into functions has several benefits:

1. A descriptive name explains the purpose of a group of statements.
2. Repeated logic can be changed in one location.
3. Small functions are easier to test with different inputs.
4. Parameters make dependencies visible instead of relying on hidden global state.

### Functions Connect the Program

Parameters and local variables rely on the concepts in [[variables-and-data-types|Variables and Data Types]]. A function can contain the branches and loops discussed in [[control-flow|Control Flow]], and it can accept the custom models described in [[structs-and-enums|Structs and Enums]]. However, passing a `String`, vector, or custom structure into a function may transfer ownership. If the caller needs to keep using the value, the function can accept a reference instead. This behavior is the focus of [[ownership-and-borrowing|Ownership and Borrowing]].

For example, `fn display_name(name: &String)` borrows a string, while `fn consume_name(name: String)` takes ownership of it. Choosing between those signatures is part of designing the function's contract.

> A function signature is a promise: it states what information the function needs and what result it provides.
