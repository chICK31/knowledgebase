---
title: Control Flow in Rust
---

# Control Flow in Rust

Control flow determines which instructions a program executes and how often it executes them. Without control flow, every statement would run once in a fixed order. Rust provides `if` expressions for decisions and `loop`, `while`, and `for` expressions for repetition. These tools turn the values described in [[variables-and-data-types|Variables and Data Types]] into behavior.

## Making Decisions with `if`

An `if` condition must evaluate to a Boolean. Rust does not automatically treat numbers or strings as true or false. This rule makes the program's intent explicit.

```rust
let hand_value = 18;

if hand_value > 21 {
    println!("Bust");
} else if hand_value == 21 {
    println!("Blackjack");
} else {
    println!("Keep playing");
}
```

Unlike in some languages, `if` is an expression and can produce a value. For example, `let result = if won { "win" } else { "loss" };` assigns one of two strings. Both branches must return compatible types because `result` must have one known type.

## Repeating Work with Loops

Rust offers three common loop forms:

- `loop` repeats indefinitely until code uses `break` or returns from the surrounding function.
- `while` repeats as long as a condition remains true.
- `for` visits each item in an iterator, collection, or range.

```rust
for round in 1..=3 {
    println!("Starting round {round}");
}
```

The `for` loop is usually the clearest choice when processing every item in a collection because it avoids manually tracking an index. A loop can also return a value with `break value`, which is useful when repeated work should stop after producing a result.

### Choosing the Right Branch

Simple Boolean decisions fit `if`, but data with several meaningful variants often fits `match`. A `match` must account for every possible case, making it especially effective with the enums covered in [[structs-and-enums|Structs and Enums]]. Repeated logic should usually be placed in [[functions|Functions]] so the loop remains readable. When a loop borrows a collection instead of consuming it, the rules in [[ownership-and-borrowing|Ownership and Borrowing]] determine whether that collection can be used afterward.

> Clear control flow makes the path through a program visible to both the compiler and the reader.
