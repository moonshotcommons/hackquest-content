# Content/**Defining the Program Module**

In this lesson, we will learn how to *define* our Solana smart program module. After completing this step, we can write the core business logic that interacts with the blockchain.

1. **Using the** `#[program]` **Macro:** This macro is used to define a Solana program module, which contains the program's instructions and other related operational functions.
    
    ```rust
    #[program]
    ```
    
2. **Defining the anchor_bac Module**:
    
    ```rust
    #[program]
    pub mod anchor_bac {}
    ```
    
    Inside this module, we will write the core business logic. Declaring it as a `pub` module ensures that the functions within it (which are the **initialization of random numbers** and **player guessing** functions we will write later) can be accessed and used externally.
    
3. **Importing Content from the Parent Module**
    
    ```rust
    #[program]
    pub mod anchor_bac {
        use super::*;
        // Subsequent business logic
    }
    ```
    
    This allows us to directly use all components defined in the parent module without needing to *declare them again*.
    

With this, our *program initialization* is complete. In the next lesson, we will learn how to write the program's random number **generation** functionality.

**Syntax** 

mod

- hint
    
    ```rust
    pub mod my_module {}
    ```