# Match

match (var) {
  (Case when var matches X condition) => Do something,
  }

```rust
fn colors(rgb: (i8, i8, i8)) {
    match rgb {
        // Can ignore tuples' variables with _ (For ease of reading's sake):
        (r, g, _) if r <= 10 && g == 10 => println!("Oh, your r is near 10, and 100% your G is a 10"),
        (_, g, _) if g == 10 => println!("Oh, your g is a 10"),
        (_, _, b) if b == 10 => println!("Oh, your b is a 10"),
        // "_" placeholder is mandatory for matches; it decides when no case matches our conditions:
        _ => println!("Nothing matched any conditions, try with other data") } }

fn matcher(input: i32) -> i32 {
    match input {
        // n @ 16 is "n" variable, which can be used as a new variable
        n @ 16 => println!("{} is 16!", n),
        _ => 0
    }
}

fn main() {
    let rgb = (10, 10, 10);
    colors(rgb);
    let rgb = (11, 12, 10);
    colors(rgb);
    let my_match = matcher(12);
    println!("{}", my_match);
    let my_match = matcher(16);
}


```
