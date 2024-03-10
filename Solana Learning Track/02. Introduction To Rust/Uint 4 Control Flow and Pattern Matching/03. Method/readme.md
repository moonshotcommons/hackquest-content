# Content

> **Introduction:** In previous sections, we learned about structs and enums, which define the properties of objects (e.g., brand, color, and price in the `Car` struct). However, having only properties is often insufficient; we also need the behavior of objects (e.g., driving, slowing down), and methods are the descriptions of these behaviors.
> 

**Methods:** These are functions associated with specific types such as structs, enums, or trait objects. They allow you to define behaviors on these types and support calling this behavior similar to invoking regular functions.

Methods are similar to functions: they use the `fn` keyword, have parameters and return values, and include logic in the function body. However, methods differ because they are defined in the context of a struct or enum using the `impl` keyword, and their first parameter is always `&self`, representing the instance on which the method is called.

- **Metaphor**
    
    Apart from the Car example mentioned earlier, let's further explain with a scenario from the Super Mario game. Mario has attributes like size, coin count, and level count. Similarly, Mario needs actions like jumping, eating mushrooms, and collecting coins. This is analogous to implementing corresponding methods on the Mario struct. Only by doing this can Mario keep progressing through levels, and our program can implement various functionalities.
    
- **Use Case**
    
    In Solana, there is a method `find_program_address` for generating [program-derived addresses (PDA)](https://docs.solana.com/developing/programming-model/calling-between-programs#program-derived-addresses). PDA are accounts derived by a program without private keys. The method returns a tuple with the first element as the generated address and the second element as the used *bump seed*.
    
    ```rust
    pub fn find_program_address(
        seeds: &[&[u8]],
        program_id: &Pubkey
    ) -> (Pubkey, u8)
    ```
    

### Documentation

In this example, a `Rectangle` struct is defined, and a `area` method is implemented on it to calculate the area of the rectangle. The method is then called in the `main` function.

```solidity
// Struct definition
struct Rectangle {
    width: u32,
    height: u32,
}

// Implementation for Rectangle
impl Rectangle {
    // The area method with &self as the first parameter, representing the instance
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

fn main() {
    let rect1 = Rectangle { width: 30, height: 50 };

    println!(
        "The area of the rectangle is {} square pixels.",
        // Calling the area method on the struct instance
        rect1.area()
    );
}
```

### FAQ

**Q1: What is the difference between methods and functions in Rust?**

A1: The main differences between methods and functions lie in their relationship with types and the way they are called.

**Methods** are associated with specific types (structs, enums, traits, etc.), defined within an `impl` block for that type, and always have `&self` as the first parameter, representing the instance on which the method is called. They are invoked using the dot operator, similar to object methods in object-oriented languages.

**Functions** are independent and not tied to any specific type. They can be defined anywhere, have no `self` parameter, as they are not associated with any particular instance, and are called directly using the function name.

**Q2: How are methods defined and used in enums in Rust?**

A2: Methods in enums are defined and used similarly to structs. See the code example below for clarification.

```rust
enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}

impl Message {
    fn call(&self) {
        match &self {
            Message::Quit => println!("退出"),
            Message::Move { x, y } => println!("移动到({},{})", x, y),
            Message::Write(text) => println!("写入{}", text),
            Message::ChangeColor(r, g, b) => println!("改变颜色为({}, {}, {})", r, g, b),
        }
    }
}

fn main() {
    let m = Message::Move { x: 1, y: 2 };
		// 调用枚举方法 call
    m.call();

    let n = Message::Write(String::from("hello"));
    n.call();
}
```

# Example

Below we show some typical scenarios in the use of structure methods: method names have the same name as fields, and associated functions.

```solidity
struct Rectangle {
     width: u32,
     height: u32,
}

impl Rectangle {
     /* Method with the same name: makes the code more consistent and concise. When you need to get or set the properties of a structure,
      * You can directly use the attribute name as the method name without additional memory or documentation, and it is more consistent.
      * Integrate intuitive reading and understanding methods to reduce the difficulty of code maintenance.
      */
     pub fn width(&self) -> u32 {
         return self.width;
     }

     //Associated function, no &self parameter
     pub fn new(width: u32, height: u32) -> Self {
         Rectangle { width, height }
     }
}

fn main() {
     // If there is no self parameter in the method, the method is an associated function.
     // Usually used to initialize instances, call the associated function new to create an instance corresponding to the structure
     let rect1 = Rectangle::new(30, 50);

     // Method 1, access the width field of Rectangle
     println!("{}", rect1.width);

     // Method 2: Call the width method of Rectangle, similar to getter()
     println!("{}", rect1.width());
}
```