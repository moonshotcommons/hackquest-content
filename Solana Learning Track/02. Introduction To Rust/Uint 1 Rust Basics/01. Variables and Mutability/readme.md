# Content

In Rust, variables can be classified into **mutable variables** and **immutable variables**. In simple terms, this classification is based on whether the value of a variable is allowed to be modified. If a variable's value can be changed after it's assigned a value in memory, it is considered a mutable variable. Conversely, if the value cannot be altered once assigned, it is an immutable variable. The former provides flexibility in programming, allowing values to change in different scenarios, while the latter, through immutability, enhances programming safety, especially in multithreaded environments, and reduces some runtime checks, thereby improving performance to some extent.

**Note:** The mutability mentioned here refers to the mutability of the **variable's value**, not the **data type** of the variable. Additionally, the concept of immutable variables is not unique to Rust; similar concepts exist in other languages like Java, where, for example, the `String` type is immutable. When operations resembling modifications are performed on an immutable object's value, a new object is essentially created, rather than modifying the value of the immutable variable.

- **Metaphor**
    
    To illustrate, consider a student named Ferris. Since Ferris's birth, the ID number is immutable, accompanying Ferris throughout its life. Immutable variables remain unchanged during their entire lifespan, offering precision in scenarios like accurate identification in a national public security system. On the other hand, details such as home address, gender (Nothing is impossible), contact information, etc., may change. These changes might be necessary for Ferris, highlighting the usefulness of immutability in certain situations.
    
    *Note: Ferris is the mascot of the Rust community, the crab cooked 🦀🙈.*
    
- **Use case**
    
    In Solana's "hello world" program (smart contract), there's a state variable `GreetingAccount` that records the number of program invocations. Each invocation increments this variable by 1. Notably, in Solana, a **program** is similar to an **smart contract** in Ethereum, with some differences. In Solana, the program does not contain data, unlike a smart contract which does. Throughout this text, we'll use the term **program** to refer to the on-chain logic of a smart contract.
    
    ```rust
    pub struct GreetingAccount {
        pub counter: u32,
    }
    
    // This is the entry function for the program (smart contract)
    pub fn process_instruction(
        program_id: &Pubkey,
        accounts: &[AccountInfo],
        _instruction_data: &[u8]
    ) -> ProgramResult {
    
        // Use mut to make greeting_account mutable when deserializing
        let mut greeting_account = GreetingAccount::try_from_slice(&account.data.borrow())?;
        greeting_account.counter += 1;
    
        Ok(())
    }
    ```
    

### Documentation

We define two variables of different types and attempt to modify their corresponding values.

```rust
fn main() {
    // x is a mutable variable; mut stands for mutable, allowing changes
    let mut x = 1;
    println!("x = {}", x);
    x = 2;
    println!("x = {}", x);

    // y is an immutable variable; Rust defaults to immutable if not specified
    let y = 3;
    println!("y = {}", y);
    // Attempting to reassign a value to an immutable variable y results in a compile-time error
    y = 4;
    println!("y = {}", y);
}
```

### FAQ

- **Q1: What are the benefits of immutable variables?**
    
    A: In Rust, variables are immutable by default (`immutable`). For such variables, the compiler performs static checks during compilation to ensure that no operations modify them within their scope. For instance, when attempting to change `y` to 4, the compiler immediately notifies that such an operation is not allowed. This static checking helps the compiler optimize code during compilation, reducing some runtime checks.
    
    For example, the compiler can embed the value of an immutable variable directly into the code during compilation, rather than accessing the variable's value through memory addressing at runtime. This can reduce memory access and loading operations, thereby improving performance.
    
- **Q2: What impact does declaring all variables as either mutable or immutable have?**
    
    A: If you don't need a variable to be mutable, defining it as mutable will result in some performance loss due to runtime checks. Conversely, if you need a variable to be mutable but declare it as immutable, you'll have to simulate mutability by continuously declaring new variables with the same name. In reality, this creates new objects in memory, leading to reduced code performance.
    
    In summary, variable mutability should be defined based on practical requirements.
    

# Example

Here we show immutable variables (default type) and mutable variables. I believe everyone is no longer unfamiliar with them🚀

```solidity

fn main() {
    // Immutable，default
    let ferris_id = 1234567890;
    println!("ferris_id_card = {}", ferris_id);

    // Mutable
    let mut ferris_address: &str = "Sunshine Beach No. 01";
    println!("ferris lived in, {}!", ferris_address);

    // reassign
    ferris_address = "Sunshine Beach No. 02";
    println!("now, ferris lived in, {}!", ferris_address);
}
```