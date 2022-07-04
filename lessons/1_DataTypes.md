Casting, primitive types, floats, data declarations

const && static

## Casting and primitive types:
```rust
// Casting and data types
fn main() {
    let my_emoji = '🌹';
    // chars only to u8 (1-255)
    let my_num = 'ú' as u8;
    println!("# {}", my_num);
    
    // Casting multiple times back and forth
    let my_char = 'ú';
    println!("> {}", my_char as char);
    println!("> {}", my_char as u8);
    println!("> {}", my_char as u8 as char as u8 as char);
    
    // Byte length vs. Character length
    let spec_char = "β"; // (β is 2 bytes, but 1 character long)
    println!("> Byte size of β: {}", spec_char.len());
    println!("> Char size of β: {}", spec_char.chars().count());
    
    data_types();
}
```
## Data types, declarations and float numbers:
```rust
fn data_types() {
    let x: usize = 12; // usize: Architecture's length (32 or 64 bit)
    // So, usize in a 64-bit computer will be u64 and so on
    //
    // type inference
    let my_var = 18; // default: i32
    let mut x = 200u8; // Or:
    let mut x = 200_u8; // Or:
    let mut t = 2_____0_________0___________u8; // Or:
    let mut x: u8 = 200;
    // Useful for:
    let my_big_number = 1_120_000_000_000__usize; // More human-readable
    // Ftr: I used usize because I have no idea what type would this number fit into
    // Or use i64/u64
    floats();
}

fn floats(){
    // f32 and f64 floating points
   let x = 5. as f32; 
   let y = 7.32; // f64 by default
   let sum = x as f64 + y as f64; // Casting and making them even
   // println!("{sum}");
}
```

## Const && Static

```rust
// type must be declared for const && static
const MY_CONSTANT: i8 = 19;
static LIST: [&str; 3] = ["hello", "world", "foo", "bar"];

fn main() {
    println!("{MY_CONSTANT}");
}
```
