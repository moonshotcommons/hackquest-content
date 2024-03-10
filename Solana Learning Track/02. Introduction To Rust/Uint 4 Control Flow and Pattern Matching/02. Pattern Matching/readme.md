# Content

**Pattern Matching:** Allows us to compare a `target` **value** with a series of **patterns** and execute the corresponding **expression** based on the matched pattern. Rust commonly uses `match` and `if let` for pattern matching. Here, we'll focus on `match` to illustrate the concept.

```java
match target {
    Pattern1 => Expression1,
    Pattern2 => {
        Statement1;
        Statement2;
        Expression2
    },
    _ => Expression3
}
```

> Note: The matching in match must be exhaustive, so we use `_` to represent all unlisted possibilities.
> 
- **Metaphor**
    
    Imagine you encounter a traffic signal while driving. The traffic signal has three colors: red, green, and yellow. Using pattern matching, you can take different actions based on the color of the signal: red, stop; green, continue; yellow, slow down. In this example, different colors of the traffic signal are like different enums, and pattern matching helps you take corresponding actions based on the signal's state.
    
- **Use Case**
    
    Consider this snippet from a Solana program about movie reviews. Users can add or update reviews:
    
    ```rust
    // Instruction type for user operations, represented as an enum
    pub enum MovieInstruction {
        // Add a movie review
        AddMovieReview {
            title: String,
            rating: u8,
            description: String,
        },
        // Update a movie review
        UpdateMovieReview {
            title: String,
            rating: u8,
            description: String
        }
    }
    
    pub fn unpack(input: &[u8]) -> Result<Self, ProgramError> {
        // Actually assign values based on the input
        let variant = 1;
        let payload;
    
        // Pattern matching
        Ok(match variant {
            0 => MovieInstruction::AddMovieReview {
                title: payload.title,
                rating: payload.rating,
                description: payload.description,
            },
            1 => MovieInstruction::UpdateMovieReview {
                title: payload.title,
                rating: payload.rating,
                description: payload.description
            },
            // Cover other cases here
            _ => return Err(ProgramError::InvalidInstructionData),
        })
    }
    ```
    

### Documentation

Here, we use `match` to match the enum type `BlockChain`. The `match` statement has three branches to fully cover all member types of the `BlockChain` enum.

```solidity
enum BlockChain {
    BitCoin,
    Ethereum,
    Starknet,
    Solana,
}

fn main() {
    let block_chain = BlockChain::Solana;
    match block_chain {
        BlockChain::BitCoin => println!("BitCoin"),
        // X | Y, similar to a logical OR, means this branch can match either X or Y
        BlockChain::Ethereum | BlockChain::Starknet => {
            println!("Ethereum or Starknet");
        },
        // Use _ to represent all unlisted possibilities
        _ => println!("Solana"),
    };
}

```

### FAQ

# Example

Here we show other uses of `match` pattern matching: pattern binding, assignment, and destructuring. `if let` simple pattern matching: used to handle situations where only the value of one pattern is matched and other patterns are ignored, which can make our code more concise.

```solidity
enum Shape {
     Circle(f64),
     Rectangle(f64, f64),
     Square(f64),
}

fn calculate_area(shape: &Shape) -> f64 {
     match shape {
         // Get the bound value from the matching pattern, such as radiux, width, side
         Shape::Circle(radius) => std::f64::consts::PI * radius * radius,
         Shape::Rectangle(width, height) => width * height,
         Shape::Square(side) => side * side,
     }
}
struct Point {
     x: i32,
     y:i32,
}

fn process_point(point: Point) {
     match point {
         Point { x: 0, y: 0 } => println!("Coordinates are at the origin"),
         Point { x, y } => println!("Coordinates are at ({}, {})", x, y),
     }
}

fn main() {
     let circle = Shape::Circle(3.0);
     let rectangle = Shape::Rectangle(4.0, 5.0);
     let square = Shape::Square(2.0);

     // 1. Call the function to output the area of each shape
     println!("The area of a circle: {}", calculate_area(&circle));
     println!("The area of the rectangle: {}", calculate_area(&rectangle));
     println!("Area of square: {}", calculate_area(&square));

     // 2. Match pattern matching for assignment
     let area = match circle {
         Shape::Circle(radius) => std::f64::consts::PI * radius * radius,
         Shape::Rectangle(width, height) => width * height,
         Shape::Square(side) => side * side,
     };
     println!("The area of the circle: {}", area);

     // 3. Deconstruct the structure
     let point1 = Point { x: 0, y: 0 };
     let point2 = Point { x: 3, y: 7 };
     process_point(point1);
     process_point(point2);

		 // 4. if let simple matching
     let some_u8_value = Some(3u8);
     match some_u8_value {
         Some(3) => println!("three"),
         // Other values besides 3 and None values should also be considered here
         _ => (),
     }
    
     //Only match the value 3
     if let Some(3) = some_u8_value {
         println!("three");
     }
}
```