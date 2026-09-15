---
title: Structs and Enums in Rust
---

# Structs and Enums in Rust

Primitive values are useful, but real programs usually need to represent concepts made from several related pieces of information. Rust provides structs for grouping fields and enums for defining a value that can be one of several variants. Together, they allow the type system to describe the program's domain instead of passing unrelated numbers and strings everywhere.

## Structs Group Related Data

A struct defines named fields. An instance must supply a value for every field, which helps prevent partially formed data.

```rust
struct Player {
    name: String,
    chips: u32,
    is_active: bool,
}

let player = Player {
    name: String::from("Hector"),
    chips: 500,
    is_active: true,
};
```

Methods can be added in an `impl` block. A method resembles one of the [[functions|Functions]], but its first parameter is often `&self` or `&mut self`. Borrowing `self` allows a method to inspect or change an instance without necessarily consuming it. Those choices follow the rules explained in [[ownership-and-borrowing|Ownership and Borrowing]].

## Enums Represent Alternatives

An enum lists every valid form a value may take. Each variant can also contain data.

```rust
enum RoundResult {
    Win(u32),
    Loss,
    Push,
}
```

Here, a win carries the number of chips earned, while a loss or push needs no additional information. This is safer and clearer than representing results with loosely related strings or special numbers.

### Handling Every Variant

The `match` expression pairs naturally with enums:

```rust
fn describe(result: RoundResult) {
    match result {
        RoundResult::Win(chips) => println!("Won {chips} chips"),
        RoundResult::Loss => println!("Lost the round"),
        RoundResult::Push => println!("Tie game"),
    }
}
```

Rust requires the match to be exhaustive, so adding a new enum variant forces relevant code to consider it. This connects custom types directly to [[control-flow|Control Flow]]. The fields and associated data still use the building blocks from [[variables-and-data-types|Variables and Data Types]], but structs and enums give those values meaning. They help make invalid states difficult—or sometimes impossible—to represent.

> Model a concept with a struct when its parts exist together; use an enum when it must be one choice among known alternatives.
