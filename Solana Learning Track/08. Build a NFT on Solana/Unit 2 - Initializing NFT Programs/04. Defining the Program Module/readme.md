# Content/**Defining the Program Module**

In this section, we're going to learn how to define our Solana program module. After completing this step, we'll be able to write the core business logic that interacts with the blockchain.

Get ready to code some magic! 🌟👩‍💻👨‍💻🚀

1. **Using the `#[program]` macro:**
    
    This macro is used to define a Solana program module, which contains the program's instructions and other related operation functions.
    
    ```rust
    #[program]
    ```
    
2. **Defining the `metaplex_nft` module:**
    
    Next, we will define a module named `metaplex_nft`. In this module, we will write the core business logic and program functions.
    
    ```rust
    #[program]
    pub mod metaplex_nft {}
    ```
    
    Declaring it as a `pub` module allows its contents to be accessed and used externally.
    
3. **Importing Contents from the Parent Module**
    
    ```rust
    #[program]
    pub mod metaplex_nft {
        use super::*;
    }
    ```
    
    This allows us to use all components defined in the parent module directly, without needing to redeclare them.
    

And that's a wrap on our program initialization! Next time, we'll dive into the fun part: crafting the core code for minting those awesome NFTs. Stay tuned! 🌟🚀💻

**Syntax** 

mod

- hint
    
    ```rust
    pub mod my_module {}
    ```
    