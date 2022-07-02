
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
