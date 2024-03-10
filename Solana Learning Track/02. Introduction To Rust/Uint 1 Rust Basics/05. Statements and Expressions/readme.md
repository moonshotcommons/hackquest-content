# Content

**Statements** in Rust are the **execution units**. They perform some operations but do not return a value, and they end with a semicolon `;`.

**Expressions** in Rust are the **computational units**. They calculate and return a value, so expressions can be used for assignments. Common expressions include function calls, macro calls, and code blocks created with curly braces.

The **unit type** in Rust is a special return value type, indicating that a function or expression doesn't return a value. It's similar to the `void` return type in other languages and is represented by the symbol `()`.

> Tip: A simple way to distinguish between statements and expressions is the presence of a semicolon `;`. If there is a semicolon, it's a statement, performing an operation without returning a result. If there is no semicolon, it's an expression, performing a calculation and returning a result. Although this method may not always hold true in certain situations, it is generally sufficient for the majority of cases.
> 
- **Metaphor**
    
    In Rust, **statements** are like the actions of a chef, such as chopping vegetables, boiling water, or seasoning. They execute tasks but don't produce the final product and end with a semicolon. **Expressions**, on the other hand, are like finished dishes, such as prepped vegetables, a pot of soup, or a prepared sauce. They calculate and return useful results that can be used for subsequent operations. Statements are the executors of tasks, and expressions are the results of calculations, together forming the dynamic process of a program.
    
- **Use case**
    
    Let's take a look at the entry point function of a Solana on-chain program (smart contract):
    
    ```rust
    // Entry point for on-chain program execution
    pub fn process_instruction(
        program_id: &Pubkey,
        accounts: &[AccountInfo],
        instruction_data: &[u8]
    ) -> ProgramResult {
    
        // This is a statement
        msg!("Hello, world!");
    
        // ...specific logic omitted
    
        // This is an expression, returning a Result::Ok type with a value of (), indicating no return value is needed
        Ok(())
    }
    ```
    

### Documentation

Let's illustrate "statements" and "expressions" with the following code:

```rust
fn main() {
    // Statement: use the 'let' keyword to create a variable and bind it to a value
    let a = 1;

    // Statement: since statements do not return a value, attempting to bind a statement (let a = 1) to variable b will result in a compilation error
    let b = (let a = 1);

    // Expression: the return value is x + 1
    let y = {
        let x = 3;
        x + 1
    };

    println!("The value of y is: {}", y); // y = 4
}

```

### FAQ

# Example

We use the following examples to learn about common statements, code block {} expressions, unit type return values, and if expressions.

```solidity
fn main() {
     //The following 4 are statements
     let a = 1;
     let b: Vec<f64> = Vec::new(); // vec means creating a dynamic array of type f64
     let (a, c) = ("hi", false); // Tuple type
     let x: i32 = 5;

     // This is a code block expression
     let y = {
         let x_squared = x * x;
         let x_cube = x_squared * x;

         //The value of the following expression will be assigned to `y`
         x_cube + x_squared + x
     };
     println!("y is {:?}", y); // y = 155

     let z = {
         // This is an expression that calculates the value of x+1 and returns
         x+1

         // If you add a semicolon (;), it becomes a statement with no return value.
         // The default in Rust is "unit type ()", at this time z = ()
         // x + 1;
     };
     println!("z = {:?}", z);
    
     // The if statement block is also an expression, so it can be used for assignment or return directly
     // Similar to the ternary operator, in Rust we can write it like this
     let p = if x % 2 == 1 {
         "odd"
     } else {
         "even"
     };
}
```