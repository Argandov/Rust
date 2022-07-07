# 

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
