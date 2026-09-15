---
title: Variables and Data Types in Rust
---

# Variables and Data Types in Rust

Variables give names to values so a program can store and use information. In Rust, a variable is immutable by default. This means its value cannot change after it is assigned. The default encourages programmers to be deliberate about which information should remain stable. For example, `let max_players = 4;` creates a value that cannot be reassigned. Writing `let mut score = 0;` adds the `mut` keyword and allows the score to change as the game progresses.

Rust can infer many types from context, but a programmer can also write the type explicitly:

```rust
let player_name: &str = "Hector";
let score: u32 = 125;
let accuracy: f64 = 87.5;
let is_active: bool = true;
```

## Scalar and Compound Types

Scalar types represent single values. Rust's main scalar types are integers, floating-point numbers, Boolean values, and characters. Integers are identified by whether they are signed or unsigned and by their size. For instance, `i32` can hold negative or positive whole numbers, while `u32` only holds nonnegative values. The distinction matters when choosing a type for information such as health, currency, or coordinates.

Compound types group multiple values. A tuple can combine different types, while an array stores several values of the same type and has a fixed length.

```rust
let card: (&str, u8) = ("Ace", 11);
let starting_hand: [u8; 2] = [10, 11];
```

### Why Types Matter

Types tell the compiler what operations are valid. A number can be added, a Boolean can control an `if` expression, and text can be passed to a display function. These checks prevent many mistakes before the program runs. Values introduced here become more useful when evaluated through [[control-flow|Control Flow]], passed into [[functions|Functions]], or stored inside [[structs-and-enums|Structs and Enums]]. Rust's rules for moving and referencing non-copy values are explored in [[ownership-and-borrowing|Ownership and Borrowing]].

> A useful type does more than store data: it communicates what that data is allowed to represent.
