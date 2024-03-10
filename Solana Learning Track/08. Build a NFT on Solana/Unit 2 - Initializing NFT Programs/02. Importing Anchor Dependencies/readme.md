# Content/Import dependencies

Welcome to the first lesson of our Solana NFT course.

In this lesson, we're going to learn how to properly import the necessary libraries and modules for our project. This is the first step in writing Solana programs, ensuring we have the right tools to write and run our code.👩‍💻👨‍💻

This course will utilize the powerful **Anchor** framework for development. Thus, the primary step is to import the relevant dependencies from the Anchor framework.

1. **Import the prelude module from `anchor_lang`**
    
    ```rust
    use anchor_lang::prelude::*;
    ```
    
    1. The **prelude** module contains the essential Anchor modules and functions we'll need for subsequent development.
    
2. **Import the `invoke` function from `anchor_lang`**
    
    ```rust
    use anchor_lang::solana_program::program::invoke;
    ```
    
    This allows our program to call another deployed external program, which will be necessary in our upcoming NFT minting operations.
    

Alright, we've successfully completed the import of Anchor dependencies. In our next lesson, we will continue with the initialization of the program. Stay tuned as we take another step forward in our Solana NFT adventure! 🚀📚👨‍💻👩‍💻

**Syntax** 

use

- hint
    
    ```rust
    use anchor_spl::token;
    ```