# Rust Control Flow

## if expression

```rust
if number % 4 == 0 {
    println!("number is divisible by 4");
} else if number % 3 == 0 {
    println!("number is divisible by 3");
} else if number % 2 == 0 {
    println!("number is divisible by 2");
} else {
    println!("number is not divisible by 4, 3, or 2");
}
```

### if in let statement

```rust
let condition = true;
let num = if condition {5} else {"six"};
```

## Loops

The loop keyword tells Rust to execute a block of code over and over again forever or until you explicitly tell it to stop.

### Normal loop

```rust
fn main() {
    loop {
        println!("again!");
    }
}
```

This prints the string "again!" infinitely unless the process is stopped by the user explicitly.

### Returning values from Loops

```rust
let mut counter = 0;
let result = loop {
    counter += 1;
    if counter == 10 {
        break counter * 2;
    }
};
println!("The result is {}", result);
```

The given snippet returns value 20 for variable "result"

### while Loop

```rust
let a = [10, 20, 30, 40, 50];
let mut index = 0;
while index < 5 {
    println!("the value is: {}", a[index];
    index += 1;
}
```

### For loop

```rust
let a = [10, 20, 30, 40, 50];
for element in a.iter() {
    println!("the value is: {}", element);
}
```

### For loop using range

```rust
for number in (1..4).rev() {
    println!("{}!", number);
}
```
