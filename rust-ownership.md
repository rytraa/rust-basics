# Rust Ownership

## Ownership

### Stack and Heap

- **Stack** is used to store variables of data type that have known size eg. u32, i32, bool, tuple(scalar types), etc. Easy to do.
- **Heap** is used to store variables of data type that do not have a known capacity Eg. String. Expensive.

String can be represented like this way

| name     | value   |
| -------- | ------- |
| ptr      | 0th idx |
| len      | 5       |
| capacity | 5       |

:arrow_down:

| idx | value |
| --- | ----- |
| 0   | h     |
| 1   | e     |
| 2   | l     |
| 3   | l     |
| 4   | o     |

- The **length** is how much memory, in bytes, the contents of the String is currently using. The **capacity** is the total amount of memory, in bytes, that the String has received from the all## Ownershipocator.

### Drop

```rust
{
    let s = String::from("hello"); // s is valid from this point forward
    // do stuff with s
} // this scope is now over, and s is no longer valid
```

When the variable goes invalid, it is **dropped**. When dropped it returns the memory address of the dropped variable, hence the space is freed for other var## Ownershipiable to use it.

### Double free memory

```rust
{
    let s1 = String::from("hello");
    let s2 = s1;
    // s1 and s2 refers to same pointer and and freed- twice
}
```

Having situations where two variables refer to same pointer, like Strings do, and Garbage Collector (GC) trying to free them twice is called Double Free Memory.

Check: [RAII - Resource acquisition is initialization](https://en.wikipedia.org/wiki/Resource_acquisition_is_initialization)

### Move

```rust
{
    let s1 = String::from("hello");
    // s1 is valid and in scope
    let s2 = s1;
    // s2 is valid, takes the value of s1.
    // s1 is invalid and out of scope. drops s1
}// s2 out of scope and drops s2
```

Hence for var stored in heap, when s2 takes value for s1, the var s1 is freed or invalid to the scope. So the GC prevents freeing twice. This similar to Shallow Copy but makes the first variable inv## Ownershipalid.

### Copy

For var stored in stack, it copies by default, instead of move.

```rust
let y: u32 = 5;
let x = y;
println('{}', y);
// The var y is valid here, because it is copied
```

### Deep copy

The copy funcionaloty can be done for var in heap as well using <code>::clone()</code> function.

```rust
let s1 = String::from("hello");
let s2 = s1::clone();
// Both s1 and s2 are valid and refers to different pointers
```

### Return Values and Scope

```rust
fn main() {
    let s1 = gives_ownership();         // gives_ownership moves its return
                                        // value into s1

    let s2 = String::from("hello");     // s2 comes into scope

    let s3 = takes_and_gives_back(s2);  // s2 is moved into
                                        // takes_and_gives_back, which also
                                        // moves its return value into s3
} // Here, s3 goes out of scope and is dropped. s2 goes out of scope but was
  // moved, so nothing happens. s1 goes out of scope and is dropped.

fn gives_ownership() -> String {             // gives_ownership will move its
                                             // return value into the function
                                             // that calls it

    let some_string = String::from("hello"); // some_string comes into scope

    some_string                              // some_string is returned and
                                             // moves out to the calling
                                             // function
}

// takes_and_gives_back will take a String and return one
fn takes_and_gives_back(a_string: String) -> String { // a_string comes into
                                                      // scope

    a_string  // a_string is returned and moves out to the calling function
}
```

---

## References

Normally, without references

```rust
fn main() {
    let s1 = String::from("hello");

    let (s2, len) = calculate_length(s1);

    println!("The length of '{}' is {}.", s2, len);
}

fn calculate_length(s: String) -> (String, usize) {
    let length = s.len(); // len() returns the length of a String

    (s, length)
}

```rust
fn main() {
    let s1 = String::from("hello");```

Using references:

```rust
fn main() {
    let s1 = String::from("hello");

    let len = calculate_length(&s1);

    println!("The length of '{}' is {}.", s1, len);
}

fn calculate_length(s: &String) -> usize {
    s.len()
}
```

The <code>&s1</code> syntax lets us create a reference that refers to the value of <code>s1</code> but does not own it. Because it does not own it, the value it points to will not be dropped when the reference goes out of scope.

### Borrowing

- We call having references as function parameters borrowing. As in real life, if a person owns something, you can borrow it from them. When you’re done, you have to give it back.

- Just as variables are immutable by default, so are references. We’re not allowed to modify something we have a reference to.

### Mutable References

```rust
fn main() {
    let mut s = String::from("hello");

    change(&mut s);
}

fn change(some_string: &mut String) {
    some_string.push_str(", world");
}
```

But mutable references have one big restriction: you can have only one mutable reference to a particular piece of data in a particular scope. **This code will fail**:

```rust
let mut s = String::from("hello");
let r1 = &mut s;
let r2 = &mut s;
println!("{}, {}", r1, r2);
```


### Data races

The benefit of having this restriction is that Rust can prevent data races at compile time. A data race is similar to a race condition and happens when these three behaviors occur:

- Two or more pointers access the same data at the same time.
- At least one of the pointers is being used to write to the data.
- There’s no mechanism being used to synchronize access to the data.

Data races cause undefined behavior and can be difficult to diagnose and fix when you’re trying to track them down at runtime; Rust prevents this problem from happening because it won’t even compile code with data races!


### Mixing mut and immut var

```rust
let mut s = String::from("hello");
let r1 = &s; // no problem
let r2 = &s; // no problem
let r3 = &mut s; // BIG PROBLEM
println!("{}, {}, and {}", r1, r2, r3);

// ERROR: cannot borrow `s` as mutable because it is also borrowed as immutable
```

### Dangling References

```rust
fn dangle() -> &String { // dangle returns a reference to a String

    let s = String::from("hello"); // s is a new String

    &s // we return a reference to the String, s
} // Here, s goes out of scope, and is dropped. Its memory goes away.
  // Danger!
```

This function's return type contains a borrowed value, but there is no value for it to be borrowed from.
