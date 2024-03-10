# Content/**Random Numbers**

In the previous lesson ***Introducing Dependencies***, we learned how to *add dependencies* to a *Rust project* and introduced the ***rand*** library, preparing to use it for **generating random numbers**. In this lesson, we will actually use the ***rand*** library to create the foundation of our project ***Bulls and Cows***: random numbers.

### **Project Workflow**

We can broadly divide the ***Bulls and Cows*** program into three parts:

- Generating random numbers
- Capturing the user's numerical input
- Determining whether the user's input matches the generated random number

In this lesson, we'll focus on the **first step**: generating a random number that can be guessed.

### **Using the *rand***

Generating random numbers is the core of the ***Bulls and Cows***. In Rust, we can easily generate random numbers using the ***rand*** library that we previously introduced.

1. **Open the main.rs**
    
    It is the main source file of the project, usually located in the `src` directory under the root:
    
    ```toml
    ├── Cargo.toml
    └── src
        └── main.rs
    ```
    
2. **Import *rand***
    
    Add `use rand::Rng;` at the top of the file. This allows us to use methods provided by the ***rand*** library in the following code.
    

**Syntax**

use

- hint
    
    ```rust
    use std::collections::HashMap;
    ```
    