# 

Functions, return values, debugging, shadowing, ownership

referencing, mutable references

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
    let x = 4;
    let x_ref = &x;
    
    let x = "Hello";
    
    println!("{}", x);
    println!("{}", x_ref);
}
```
In-Scope and out of scope shadowing

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

Shadowing, referencing and address location (Same as first Shadowing example but with more information):

```rust
// Taking a variable, assigning another to its reference, shadowing it and showing its memory address
fn main() {
    // First Var and its Address in mem:
    let var = String::from("X is an X");
    println!("# {:p} | Variable's Address", &var);
    let var_ref = &var;
    println!("# {:p} | Variable reference's Address", &var_ref);
    
    // Shadowing the original Var twice and showing its memory:
    let var = 12; 
    println!("# {:p} | 1 Shadowing variable's Address", &var);
    let var = 120; 
    println!("# {:p} | 2 Shadowing variable's Address", &var);
    //
    println!("{var}"); // Original var got shadowed (twice)
    println!("{var_ref}"); // Original reference is still intact
}

```

## References & De-references, mutable references

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

fn main() {
    let mut x = 1;
    let x1 = &mut x; // Mutable Reference
    *x1 += 10;
    
    println!("{}", x1);
}

```

## Ownership & Functions

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

// Used for stack values (Values "known at compile time")
fn to_copy(val: &str) -> &str {
    println!("> {} was copied", val);
    val // Simply return the same value
}
```

```rust
fn main() {
    let my_val = String::from("Hello world");
    let x: &str = &my_val; // Borrowed my_val, so it is still valid
    let x = &my_val; // Second option, 

    println!("{}", x);
    println!("{}", my_val); // my_val is still valid
}
```

Passing Pointers of Vars to functions to keep ownership:
```rust
fn main () {
    let x = String::from("hello");
    print(&x); // Passing only the pointer to the function
    
    // The variable didn't change ownership
    println!("b) <{}> From main() Function.", x);
}

fn print(x: &String) {
    println!("a) <{}> From inside print() function", x);
}
```
