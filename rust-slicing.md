# Rust Slicing

## Examples

```rust
let s = String::from("hello");
// Equivalent 1
let slice = &s[0..2];
let slice = &s[..2];
// Equivalent 2
let len = s.len();
let slice = &s[3..len];
let slice = &s[3..];
// Equivalent 3
let slice = &s[0..len];
let slice = &s[..];
```

## String slices as Params

A more experienced Rustacean would write the signature as it allows us to use the same function on both <code>&String</code> values and <code>&str</code> values.

```rust
fn first_word(s: &str) -> &str {
```

## Other Slices 

```rust

let a = [1, 2, 3, 4, 5];
let slice = &a[1..3];
assert_eq!(slice, &[2, 3]);
```
