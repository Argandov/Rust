Printing & pretty printing

## Memory & byte size for types:

Using [std::mem memory module functions](https://doc.rust-lang.org/std/mem/index.html#functions) (From official docs)

```rust
// Memory & byte size for default types:
fn main() {
    let v1 = std::mem::size_of::<String>();
    println!("Strings are {:?} bytes long",v1);
    
    let v1 = std::mem::size_of::<&str>();
    println!("&str's are {v1} bytes long");
    
    let v1 = std::mem::size_of::<i8>();
    println!("i8's are {v1} bytes long");
    
    let v1 = std::mem::size_of_val("β");
    println!(r#"> &str "β" is {v1} bytes long"#);
    
    let v0 = String::from("β");
    let v1 = std::mem::size_of::<v0>();
    println!(r#"> String "β" is {v1} bytes long"#);
}
```
---

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

## Pretty printing

```rust
fn main() {
    // Quick referencing variables inside a print statement:
    println!("My name is {name} {lastName}, and I'm {age} y.o",
        name = "Jean",
        lastName = "Serz",
        age = 189
    );
    
    // Using variables more than once inside print statements
    let country_i_like = "France";
    let favourite_country = "Australia";
    println!(
    "I like {0}, but I like {1} more. {1} is better than {0}", 
        country_i_like, 
        favourite_country
        ); // Or:
    
    // Ugly way of doing things:
    let x = 16;
    println!("{} is at {:p} and its value in hex is {:x}", x,&x,x);
    
    // Printing with paddings:
    let t = "Hi!";
    println!("{:_>16}", t); // _____________Hi!
    println!("{:_^16}", t); // ______Hi!_______
    println!("{:_<16}", t); // Hi!_____________
    
    let a = "dog";
    println!("{:*>4}",a); // 4 is the total length (-> *dog)
        
    let pipe = "|";
    println!("{: <2}{: >2}",pipe,pipe); // Simply 2 buffers of 2 chars -> "|  |"
    
    // Horrible:
    println!(
"Name: {Name_Variable:->10}
Second Name: {Second_Name:->10}",
        Name_Variable = "Jean",
        Second_Name = "Soltz");
    // Name: ------Jean
    // Second Name: -----Soltz 
        
        
        
    // Better:
    let Name = "Jean";
    println!("{Key:_<10}{Value:_>10}",
    Key = "Name:",
    Value = Name); // Name:___________Jean
}
```
    println!(r#"C:\Users\text.txt"#);



        ); // Or:
