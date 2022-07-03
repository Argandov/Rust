# 

Functions, return values, debugging, referencing, shadowing

## Functions, return values and debugging

```rust
fn main() {
    // Using return values for tuples:
    let t1 = make_tuple();
    println!("{}", t1.0);
    println!("{}", t1.1);
    block();
}

fn make_tuple() -> (i8, i8) {
    (12, 32) // NO semicolon here. That would terminate the function and 
            // not return anything
}

fn block() {
    // mindfuck: Just to demo a function inside a codeblock inside a function:
    let x = {
        fn hello_world() -> usize { 1200 }
        let y = hello_world();
        y
    }; // x = y = 1200
    
    println!("{}", x);
    deb();
}

// Debug printing
fn deb() {
    let my_num = { 12; };
    println!("{}", my_num); // "help: the trait `std::fmt::Display` is not implemented for `()`"
    println!("{:?}", my_num); // my_num = () (Can't use display, not a type)
    // Instead of throwing an error, it will print whatever the var is (Even though
        // it cannot use 'Display')
}
```

## Shadowing
Shadowing: re-assigning a variable twice with the same name
```rust
fn main() {
    let x = 12;
    {
        println!("{x}"); // Before shadowing (12)
        let x = 32;
        println!("{x}"); // After Shadowing (32)
    }
    println!("{x}"); // It never changed its value in this scope (12)
    println!("-------------");
    
    //
    let v = shadower();
    println!("{v}");
}

fn shadower() -> i8 {
    let v = 1;
    println!("{v}");
    let v = 2;
    println!("{v}");
    v
}
```

## References & De-references

```rust
fn main() {
    // References (&) and de-references (*)
    let x = 12;
    let Rx = &x; // (Reference of x)
    let RRRx = &&&x; // (Reference of the reference of the reference of x)
    println!("{}", *Rx == x); // true; reference, de-referenced
    // println!("{:?}", ***RRRx == x ); // Error: can't compare 
    println!("{:?}", ***RRRx == x ); // true (De-referenced 3 times = original value)
    println!("{}", RRRx); // 12
}
```