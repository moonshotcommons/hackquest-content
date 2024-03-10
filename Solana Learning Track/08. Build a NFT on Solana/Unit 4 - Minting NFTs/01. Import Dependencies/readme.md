# Content/Import Dependencies

Ready to start our NFT minting journey? 🚀 🚀  

First, we'll import the anchor_spl library. It's our key to interacting with the Solana Standard Program Library (SPL), simplifying token management and other functions.

1. **Begin by importing the `anchor_spl::token` module.**
    
    ```rust
    use anchor_spl::token;
    ```
    
    This module integrates Solana's token standards into our toolkit, equipping us for a range of token operations. It simplifies tasks such as creating, transferring, and querying tokens.
    
2. **Now, import the `MintTo` and `Token` structs from `anchor_spl::token`.**
    
    ```rust
    use anchor_spl::token::{MintTo, Token};
    ```
    
    Here's the breakdown:
    
    - ***MintTo*：** This is our tool for minting new tokens, a critical function in our NFT journey.
    - ***Token*：** Consider this as the core representation of a token in our code.
    
    Together, these structures form the backbone of our NFT minting code.
    

In the upcoming lessons, we're going to have some fun putting these imports to use. 🚀 Get ready to see how they power up our NFT minting skills! 💪🎨

**Syntax** 

use

- hint
    
    ```rust
    use anchor_spl::token;
    ```