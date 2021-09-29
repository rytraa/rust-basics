# Rust Functions

## Functions

```rust
fn main() {
    another_function(5, 6);
}

fn another_function(x: i32, y: i32) {
    println!("The value of x is: {}", x);
    println!("The value of y is: {}", y);
}
```

### Expression

- Returns a value
- Calling a function is an expression.
- Calling a macro is an expression

```rust
let y = {
    let x = 3;
    x + 1
};
```

Here it returns value 4

### Return Value

```rust
fn five() -> i32 {
    5
}

fn main() {
    let x = five();
    println!("The value of x is: {}", x);
}
```
