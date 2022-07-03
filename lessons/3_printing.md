Printing & pretty printing

## Raw printing, unicode and UTF-8

```rust
// Escaping and printing different data types

fn main() {
    println!(r"\n \t not escaped");
    println!(r"C:\Users\text.txt"); // is the same as using #:
    println!(r#"C:\Users\text.txt"#);
    
    // Escaping pound signs and double quotes:
    println!(r##"The hashtag is #hello"##);
    println!(r###"I can use ## now"###); // Double ## inside a triple ### raw string
    println!(r#"Some say, "Quotes won't matter""#); // Quotes inside string
    
    // Bytes
    println!("{:?}", b"AAA"); // Printing bytes with debug printing
    println!("{:#?}", b"AAA"); // Pretty printing debug
    
    // Hex printing & unicode
    println!("{:X}", 'A' as u32);
        // Not using char because  we need to convert i2t to Dec, and then to Hex
        // A -> 65 Dec -> 41 Hex
    println!("> \u{41}"); // A (Unicode of 41)
}

```
## Address location, binary, hex, octal
```rust
fn main() {
    let x = 1;
    println!("Original: {}\nBinary: {:b}\nHex: {:x}\nOctal: {:o}", x,x,x,x);
    
    // println!("{:p}", x); // Error: the trait `Pointer` is not implemented for `{integer}`
    println!("\nAddress Location: {:p}", &x); // Exact address of the pointer
}
```
