Loops, while loops, for llops

Ranges

# Loops

```rust

// Endless loops with no name:

fn normal_loop() {
  loop {
    println!("hello");
      {
  }
```

Returning "break" with a value:

```rust
fn main() {
    let mut my_vec = Vec::new();
    for i in 0..=100 {
        my_vec.push(i);
    }
    
    let mut counter: i8 = 0;
    let my_value = loop {       // break counter will assign to "my_value"
        counter += 1;
        if counter == 10 {
            break counter       // Return variable "counter"; assign it to "my_value"
        };
    };
    println!("# FINAL VALUE: {my_value}");    
```


// Naming Loops

`'my_loop: loop {}`
`(...) break 'my_loop;`

```rust


fn main() {
    let mut c1 = 0;
    let mut c2 = 0;
    
    println!("FIRST LOOP");
    'loop1: loop { // Naming our first Loop
        println!("{c1}");
        c1 += 1;
        if c1 == 3 {
            println!("SECOND LOOP");
            'loop2: loop { // Naming our second, nested loop
                println!("{c2}");
                c2 += 1;
                if c2 == 4 {
                    break 'loop1; // Breaking loop 1, which is the root loop
                }
            }
        }
    }
}
```

# WHile Loops

-> Basic syntax: `while condition {} `

```rust
while counter < 10 { }
```

# For Loops

fn main() {
    let mut my_vec = Vec::new();
    for i in 0..=100 {
        my_vec.push(i);
    }
    
    for number in my_vec {
        println!("> 0-100 Counter: {number}");
    }
    
}

# Ranges

Exclusive ranges: 
`for i in 0..1_000 {} ` (0 -> 999)

Inclusive Ranges:
`for i in 0..=1_000` (0 -> 1000)

Rust compiler doesn't like unused variables.
Note: If we aren't using a variable, we can name them as "_":
`for _ in 0..=1_000 {}`
