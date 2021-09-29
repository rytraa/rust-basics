# Rust Data Types

## Scalar data types

### Integer Size

| Length  | Signed | Unsigned |
| ------- | ------ | -------- |
| 8-bit   | i8     | u8       |
| 16-bit  | i16    | u16      |
| 32-bit  | i32    | u32      |
| 64-bit  | i64    | u64      |
| 128-bit | i128   | u128     |
| arch    | isize  | usize    |

### Integer Literals

| Number literals | Example     |
| --------------- | ----------- |
| Decimal         | 98_222      |
| Hex             | 0xff        |
| Octal           | 0o77        |
| Binary          | 0b1111_0000 |
| Byte (u8 only)  | b'A'        |

### Boolean

```rust
let t = true;
let f: bool = false;
```

### Character

```rust
let c = 'X';
let x:char = '
```

## Tuples

### Declaration and Accessing

```rust
let tup: (i32, f64, u8) = (500, 6.4, 1);
let five_hundred = x.0;
let six_point_four = x.1;
let one = x.2;
```

### Destructuring

```rust
let tup = (500, 6.4, 1);
let (x, y, z) = tup;
println!("The value of y is: {}", y);
```

## Arrays

### Declaration

```rust
let months = ["January", "February", "March", "April", "May", "June", "July",
              "August", "September", "October", "November", "December"];
```

### Explicit declaration

```rust
let a: [i32; 5] = [1, 2, 3, 4, 5];
```

### Alter. syntax

```rust
// let a = [3,3,3,3,3]
let a = [3;5];
```
