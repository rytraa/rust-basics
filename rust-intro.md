# Rust Introduction

## Input and Output

### Output

- println!() is a macro
- The ! mark refers to a macro

```rust
println!("Hello World!");
```

### Input

- The input is received as following
- read_line() -> returns **io::Result**, which is an enum
- if not called with expect(), considers io::Result as **Err** variant
- variables immutable by default

```rust
use std::io;
let mut guess;
io::stdin()
    .read_line(&mut guess)
    .expect("Failed to read the value");
```

### Placeholders

```rust
println!("Numbers are {} and {}", 5, 4);
```

### Range Expression

- start..end
- eg:

```rust
use rand::Rng;
let secret = rand::thread_rng().gen_range(1..101);
```

### Match

- Consist of **"Arms"**, which are the possible outcomes of match

```rust
match guess.cmp(&guessed){
    Ordering::Less => println!("Too small!"),
    Ordering::Greater => println!("Too big!"),
    Ordering::Equal => println!("You win!"),
}
```

### Loop

```rust
use rand::Rng;
use std::cmp::Ordering;
use std::io;

fn main() {
    println!("Guess the number!");
    let guessed = rand::thread_rng().gen_range(1..10);
    loop {
        let mut guess = String::new();
        io::stdin()
            .read_line(&mut guess)
            .expect("Failed to read the value");
        println!("You guessed: {}", guess);
        let guess: u32 = match guess.trim().parse() {
            Ok(num) => num,
            Err(_) => continue,
        };
        match guess.cmp(&guessed) {
            Ordering::Less => println!("Too small!"),
            Ordering::Greater => println!("Too big!"),
            Ordering::Equal => {
                println!("You win!");
                break;
            }
        };
    }
}

```
