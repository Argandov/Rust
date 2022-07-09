Structs vs Enums

Structs are multiple values (Val1 AND Val2), while Enums are choices for a value (Val1 OR Val2)

---
# Structs 

Multual referencing: From struct PersonInfo to Coordinates
```rust
struct FileDirectory;
struct Coordinates(u8, u8, u8);

struct PersonInfo {
    name: str,
    age: u8,
    location: Coordinates
}

fn main() {
    let myCoordinates = Coordinates(187, 12, 12);
    let yourCoordinates = Coordinates(12, 198, 1);
    
    let myInfo = PersonInfo { 
        name: "Git",
        age: 18,
        location: yourCoordinates
    };
    println!("{}", myInfo);
} 
```

```rust
struct Country {
    population: i32,
    name: &str
    }
```

## Struct; Debug printing

To be able to print our new structs:
```rust
// DEBUG RINTING:

#[derive(Debug)] // To be able to print (:?), the "Debug" type must be available
struct Hex (u8, u8, u8);

#[derive(Debug)] // To be able to print (:?), the "Debug" type must be available
struct Colour {
    name: String,
    hex: Hex
}


fn main() {
    let my_color_hex = Hex(12,12,12);
    let my_color = Colour {
        name: String::from("red"),
        hex: my_color_hex
    };
    println!("{:?}", my_color) // Debug printing
    
}
```

---

# Enum

List of choices or algebraic data types

```rust
// Simple Day / Night enum:
// Based on time of day (let my_time: i8), fall into a struct value and then
// decide. In this case, simply print based on this match

enum Time {
    Day,
    Night
}

fn main() {
    let my_time = 1;
    let day_state = determine_time(my_time);
    announce_time(&day_state);
}

fn determine_time (my_time: i8) -> Time {
    match my_time {
    // Simply return a Day state enum value
        6..=19 => Time::Day,
        _ => Time::Night
    }
}

fn announce_time (day_time: &Time) {
    match day_time {
    // Use the state enum value to decide what to do in each case
        Time::Day => println!("IT's day!"),
        Time::Night => println!("It's NIGHT!")
    }

```
Assigning values to enum types:
```rust
// Simple program that takes a positive or negative number, checks is it's positive, 
// assigns the result into a Vec, and then decide if it's U32 or an I32

enum Number {
    U32(u32), //Assigning type
    I32(i32)
}

fn main() {
    let x = get_num(-10);
    let y = get_num(120);
    let my_vec = vec![x, y];
    use Number::*;
    for v in my_vec {
        match v {
            U32(n) => println!("{n} is a U32"), // Using U32(n) for completeness;
                // U32 alone would lack a type
            I32(n) => println!("{n} is an i32")
        }
    }
}

fn get_num(num: i32) -> Number {
    match num.is_positive() {
        true => Number::U32(num as u32),
        false => Number::I32(num)
    }
}
```

Enum values:
```rust
// Just like Lists, each item has a value starting at 0
// Unless we assign a new value (Car is still 0, pen is 12, 
// everything else starts at 12 - mouse is 13)
enum Things { car, pen = 12, mouse, laptop }

fn main() {
    let thing = Things::pen;
    println!("{:?}", thing as u8); // 12
    let thing = Things::car;
    println!("{:?}", thing as u8); // 0
    let thing = Things::mouse;
    println!("{:?}", thing as u8); // 13
```

## Importing enums
(Ease of use)
```rust
enum Web {
    WASM,
    React,
    NodeJS,
    TS,
    Flask,
    Django,
    HTML,
    CSS,
    Javascript
}

// --snip--
use Web::*;
match my_val {
    // Instead of calling Web::Django, etc.
    Django => 0, 
    NodeJS => 1,
    TS => 2,
    WASM => 3
}
```


