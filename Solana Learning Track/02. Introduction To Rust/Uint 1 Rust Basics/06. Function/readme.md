# Content

**Functions** are a common concept in programming. They represent a reusable block of code used to perform specific tasks or operations. Functions can take input parameters (optional), perform a series of operations, and return a value (optional).

> It's important to note that in Rust, function and variable names follow the ***snake_case*** naming convention. In snake_case, all letters are lowercase, and words are separated by underscores. While languages like Java and JavaScript follow the CamelCase naming convention, if camel case is used in Rust, the program will still run, but the code might look a bit odd~👀
> 
- **Metaphor**
    
    Functions in programming languages are conceptually similar to mathematical functions (e.g., y=f(x)), where an output value is calculated based on input values. Just as there are various functions like quadratic, cubic, and polynomial functions in mathematics, programming functions also come in various forms. Let's explore further.
    
- **Use Case**
    
    When discussing functions, it's necessary to introduce the entry point function `process_instruction` in Solana. This function serves as the entry point for program execution:
    
    ```rust
    // Mark process_instruction function as the entry point for the program
    entrypoint!(process_instruction);
    
    // Function name follows snake_case naming convention
    pub fn process_instruction(
        // Parameters must explicitly specify types
        program_id: &Pubkey,
        accounts: &[AccountInfo],
        instruction_data: &[u8]
        // Function return type is the ProgramResult enum
    ) -> ProgramResult {
        msg!("Hello, world!");
    
        Ok(())
    }
    
    // Return type is an enum with variants of Result type
    enum ProgramResult {
        // You can omit the Result:: prefix and directly use OK
        Ok(()),
        // Err value is still an enum type
        Err(ProgramError),
    }
    
    // Error enum
    pub enum ProgramError {
        Custom(u32),
        InvalidArgument,
        InvalidInstructionData,
        // ...
    }
    ```
    

### Documentation

Now let's take a look at the various components of a function. It's important to note that **function parameters need explicit type annotations**. This not only improves code readability but also helps Rust provide stronger type safety, assisting the compiler in discovering errors when types don't match and providing useful error messages.

```rust
// 'fn' is the keyword for declaring a function
// 'unsafe_add()' is the function name, following the snake_case convention
// 'i' and 'j' are input parameters, and their types need to be explicitly specified
// --> 'i32' indicates the return type is also of type 'i32'
fn unsafe_add(i: i32, j: i32) -> i32 {
    // This is an expression, so the function will return this value after computing the sum
    i + j
}

```

In the previous sections, we learned that integer addition might result in **overflow**, but here there's no special handling, so `unsafe_add` serves as a reminder to developers that this addition is unsafe, and caution is needed~.

### FAQ

**Q1: Why did Rust design the unit type `()` with no return value?**

A: Rust is a statically typed language, and it needs to determine the return type of each function at compile time. When there are no return statements or expressions in the function body, the compiler cannot determine what the return type of the function should be. To address this issue, Rust introduced the unit type `()` as a special type, representing functions that don't return a value. Similar to the `void` type in other languages, it is typically used for operations like printing messages or writing to files that don't require a return value.

**Q2: What are Diverging Functions?**

A: Diverging functions refer to functions that never return, not even the default `unit type ()` return value. These functions are usually marked with the `!` type. They are commonly used for handling errors or unrecoverable situations, expressing this state by terminating the program's execution.

# Example

We show here some Rust-specific functions: expressions as functions that return a value, unit types `()` as functions that return a value, and divergent functions that never return.

```rust
// Expression as a function that returns a value
fn max_plus_one(x: i32, y: i32) -> i32 {
     if x > y {
         // If this rule is hit, you can return directly through return
         return x + 1;
     }

     //The last line is an expression, which can be used as a function return value
     // Note that there cannot be a semicolon here, otherwise it will be a statement
     y+1
}

// Unit type () as a function that returns a value
// This function does not have an explicit return value type, and Rust returns the unit type () by default
fn print_hello() {
     // This is a statement, not an expression
     println!("hello");
}

// A divergent function that never returns, marked with !
fn diverging() -> ! {
     // Throw a panic exception and terminate the program.
     panic!("This function will never return!");
}
```