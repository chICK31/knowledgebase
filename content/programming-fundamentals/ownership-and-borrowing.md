---
title: Ownership and Borrowing in Rust
---

# Ownership and Borrowing in Rust

Ownership is Rust's system for managing memory safely without relying on a garbage collector. The central idea is that every value has an owner. When the owner leaves scope, Rust automatically drops the value and releases its resources. Simple values such as many integers implement the `Copy` trait, so assigning them to another variable copies the data. Heap-allocated values such as `String` usually move instead.

```rust
let first = String::from("ApexLite");
let second = first;
// println!("{first}"); // Error: first was moved.
println!("{second}");
```

The move prevents two variables from trying to free the same allocation. It can initially feel strict, but the compiler is preventing a real class of memory errors before the program runs.

## Borrowing with References

A reference allows code to access a value without taking ownership. An immutable reference uses `&T`, and a mutable reference uses `&mut T`. Rust permits many immutable references or one mutable reference at a given time, but not both simultaneously. This rule prevents data races and unexpected mutation.

```rust
fn title_length(title: &String) -> usize {
    title.len()
}

let title = String::from("Rust Fundamentals");
let length = title_length(&title);
println!("{title} has {length} characters");
```

![[assets/ownership-borrowing-flow.svg|A three-step diagram showing a String owned by main, borrowed by a function, and then used again by main]]

*The function temporarily borrows the `String`; ownership remains with `main`, so the original value is still available afterward.*

### Ownership as a Flow

1. `main` creates and owns the `String`.
2. `&title` lends read-only access to `title_length`.
3. The reference ends after the function call.
4. `main` can continue using `title` until its scope ends.

Ownership affects the parameters and return values in [[functions|Functions]]. It also controls how collections are processed through [[control-flow|Control Flow]] and how fields behave inside [[structs-and-enums|Structs and Enums]]. Understanding the underlying types from [[variables-and-data-types|Variables and Data Types]] helps explain why an integer may copy while a `String` moves.

> Borrowing is temporary access, not shared ownership of the resource.

## Further Reading: RustViz (PDF)

The paper *RustViz: Interactively Visualizing Ownership and Borrowing* explains a teaching tool that displays ownership and borrowing events along a timeline. Its examples connect the rules above to the lifetime of each value and reference.

![[assets/rustviz-ownership-and-borrowing.pdf]]

[Open or download the PDF](../assets/rustviz-ownership-and-borrowing.pdf) if your browser does not display the embedded viewer.

**Source:** Gongming (Gabriel) Luo, Vishnu Reddy, Marcelo Almeida, Yingying Zhu, Ke Du, and Cyrus Omar (2020). *RustViz: Interactively Visualizing Ownership and Borrowing*. [arXiv:2011.09012](https://arxiv.org/abs/2011.09012).

**Image source:** Original ownership-and-borrowing diagram created for this knowledge base.
