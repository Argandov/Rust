# Data types

```rust
// Data types

fn main() {
    let integer = 1;
    let floatNum = 13.12;
    let myString = "hello world";
    let myList = [1, 2, 4];
    let myTuple = (1, 2, 3);

    // Create vas on the fly
    let myNumber = myList[1];
    let (x, y, z) = myTuple; 

    println!("{}", z);
    println!("{}", myNumber);

    printer("hello world!")
}

// Specifying integer size (Can be called with adder(6);) "i8 -> integer 8 bit"
fn adder(x: i8){
    println!("{}", x + x);
}

// Specifying type of arg, and disregarding byte size with &type
fn printer(msg: &str){
    println!("{}", msg);
}

fn types() {
    let x: u8 = 255; // Integer, unsigned, 1 byte max
    let y: u16 = 65535; // max 2 byte
    let y_n: i16 = -32768; // max 2 byte - 1 bit for signing (+/-)000 0000 0000 0000
    let y2: i8 = -120;

    let _my_tuple: (i8, char, f32) = (12, 's', 12.3);
    let _var_dump = _my_tuple.1;
    let _my_message: &str = "Hello World!";

    for c in _my_message.chars(2:) {
        println!("{}", c);
    }

    println!("{}", _my_message);

    let _f_n: f32 = 2.55; // floating 32 or 64 bit only

    let _my_bool: bool = true;
    
    let _my_char: char = 's';
}
```
---

# Ownership & Functions

```rust
// Demo: How Stack & Heap values get deallocated when reassigned to other variables
// a) s gets allocated into the Heap, while y gets into the stack
// b) Functions take ownership of heap values, they get dropped, and cannot be used again further. 
// The workaround is to return a value again by the function

fn main() {

    let s = String::from("Hello"); // This will be valid until stealer() takes ownership
    let y = "World"; // This can be used infinitely under main() scope
    println!("> {}", s); // Still valid
    
    let X = stealer(s); // s is not valid anymore because stealer() took ownership
    println!("now: > {}", X); // X is the new s
    
    let y2 = to_copy(y); // s is not valid anymore because stealer() took ownership
    println!("now: > {}", y); // y is still on the stack
    println!("now: > {}", y2); // y is still on the stack
}

// Used for String type
fn stealer(val: String) -> String {
    println!("{} - Was Stolen", val);
    val // Simply return the same value
}

// Used for stack values
fn to_copy(val: &str) -> &str {
    println!("> {} was copied", val);
    val // Simply return the same value
}



```
