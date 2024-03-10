# Content

**Enums :** A user-defined data type in Rust that allows you to enumerate possible values, also known as **variants**, where each variant can contain different types of data. Enums are primarily used to represent different options or operations, facilitating pattern matching scenarios. Its definition is as follows:

```rust
enum EnumName {
    Variant1,
    Variant2,
    ……
}
```

- **Metaphor**
    
    The concept of enums can be likened to "traffic signal lights," having three different values: red, green, and yellow. Similarly, "days of the week" can be considered an enum, consisting of seven values ranging from Monday to Sunday. In simple terms, enumerating all possible values in a domain forms its enum type.
    
- **Use Case**
    
    In Solana, `ProgramError` is used to define error types for on-chain programs.
    
    ```rust
    pub enum ProgramError {
        // Custom error code
        Custom(u32),
        // Invalid argument error
        InvalidArgument,
        // Invalid instruction data error
        InvalidInstructionData,
        ……
    }
    ```
    

### Documentation

Let's take a traffic light as an example to see what its enum looks like.

```solidity
// Defined using the enum keyword
enum TrafficLight {
  // Enumerating all possible values here
  Red,
  Yellow,
  Green,
}
```

### FAQ

**Q: What is the Option enum, and how is it used?**

A: The Option enum is primarily used to handle cases where a value might be absent, avoiding runtime errors caused by using null pointers. Its definition is as follows:

```rust
// It has two enum values, Some(T): Contains a specific value T, and None: Represents no value.
enum Option<T> {
    None,
    Some(T),
}
```

In the example below, the return value of the `divide` function is the `Option` enum. Note that in Rust's standard library `prelude`, the Option enum is automatically imported, so there's no need to explicitly use the `Option::` prefix or explicitly import it using the use statement when using Option in code.

```rust
//Define a function and return an Option enumeration
fn divide(x: f64, y: f64) -> Option<f64> {
    if y == 0.0 {
        None
    } else {
        Some(x / y)
    }
}

fn main() {
		// Call the function and match the variant of Option
    let result1 = divide(10.0, 2.0);
    match result1 {
				// No need to explicitly use Option::Some(data) here
        Some(data) => println!("result1:{:?}", result1),
        None => println!("result1: None"),
    }

		// When the denominator is 0, return None value
    let result2 = divide(10.0, 0.0);
    match result2 {
        Some(data) => println!("result2:{:?}", result1),
        None => println!("result2: None"),
    }
}
```

# Example

Here we learn the use of enumerations and how enumerations express more information.

```solidity
// Simple enumeration
enum TrafficLight {
     Red,
     Yellow,
     Green,
}

// An enumeration containing values, different members can hold different data types
enum TrafficLightWithTime {
   Red(u8),
   Yellow(char),
   Green(String),
}

fn main() {
     // Access members of TrafficLight through the :: operator
     let red = TrafficLight::Red;
     let yellow = TrafficLight::Yellow;

     // Traffic light containing time
     let red_with_time = TrafficLightWithTime::Red(10);
     let yellow_with_time = TrafficLightWithTime::Yellow('3');
     let green_with_time = TrafficLightWithTime::Green(String::from("Green light lasts for 30 seconds"));
}
```