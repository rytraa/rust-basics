# Rust Structs

A struct, or structure, is a custom data type that lets you name and package together multiple related values that make up a meaningful group.

```rust
struct User{
    username: String,
    sign_in_count: i64,
    active: bool,
}

let user1 = User {
    username: String::from("John Doe"),
    sign_in_count: 1,
    active: false,
};
```

## Using Functions

```rust
fn build_user(email: String, username: String) -> User {
    User {
        email: email,
        username: username,
        active: true,
        sign_in_count: 1,
    }
}
```

### Using the Field Init Shorthand when Variables and Fields Have the Same Name

```rust
fn build_user(email: String, username: String) -> User {
    User {
        email,
        username,
        active: true,
        sign_in_count: 1,
    }
}
```

## Struct update syntax

The code creates an instance in user2 that has a different value for email and username but has the same values for the active and sign_in_count fields from user1.

```rust
let user2 = User {
    username: String::from("anotherusername567"),
    ..user1
};
```

## Tuple Structs

```rust
struct Color(i32, i32, i32);
struct Point(i32, i32, i32);
let black = Color(0, 0, 0);
let origin = Point(0, 0, 0);
```

## Printing structs

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };
    println!("rect1 is {:?}", rect1);
}

// rect1 is Rectangle { width: 30, height: 50 }
```

## Method Syntax

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!(
        "The area of the rectangle is {} square pixels.",
        rect1.area()
    );
}
```

### Automatic Referencing

```rust
p1.distance(&p2);
(&p1).distance(&p2);
```

The first one looks much cleaner. This automatic referencing behavior works because methods have a clear receiver—the type of self. Given the receiver and name of a method, Rust can figure out definitively whether the method is reading (&self), mutating (&mut self), or consuming (self).

### With params

```rust
impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }

    fn can_hold(&self, other: &Rectangle) -> bool {
        self.width > other.width && self.height > other.height
    }
}
```

### Associated functions

- Methods of <code>impl</code> blocks that dont take self as a parameter.
- Often used for constructors that will return a new instance of the struct.

```rust
impl Rectangle {
    fn square(size: u32) -> Rectangle {
        Rectangle {
            width: size,
            height: size,
        }
    }
}
```

