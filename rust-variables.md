# Rust Variables

## Mutability

- Immutable by default

```rust
//let var_name: type = value;
let pet: String = "🐶🐕";
```

- To make it mutable

```rust
let mut pet: String = "🐶🐕";
pet = "🐱‍👤🐱";
```

## Constants

```rust
const MAX_POINTS: u32 = 100_000;
```

## Shadowing

This program first binds x to a value of 5. Then it shadows x by repeating let x =, taking the original value and adding 1 so the value of x is then 6. The third let statement also shadows x, multiplying the previous value by 2 to give x a final value of 12.

```rust
let x = 5;
let x = x + 1;
let x = x * 3;
println!("The value of x is: {}", x);
```

Difference between a mutable variable and shadowing is that, since in shadowing, the variable is re-declared/reassigned, it can change its type. But in **mut** we’re not allowed to mutate a variable’s type.


