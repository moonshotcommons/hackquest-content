# Content/**Defining the `token_program` Attribute**

In this lesson, we're going to add another important attribute to our ***MintNFT*** struct: the ***token_program***. This attribute refers to the program handling token-related operations and plays a key role in our NFT minting process.

**Adding the *token_program* Attribute:**

```rust
#[derive(Accounts)]
pub struct MintNFT<'info> {
    #[account(mut)]
    pub mint_authority: Signer<'info>,
    #[account(mut)]
    pub mint: UncheckedAccount<'info>,
    pub token_program: Program<'info, Token>,
}
```

`Program<'info, Token>`：The field ***token_program*** is of type `Program` and represents a program on Solana, The generic `Token` specifies that it is responsible for executing all token-related operations, such as token transfers and minting.

**Syntax** 

macro struct

- hint
    
    ```rust
    #[derive(Accounts)]
    pub struct MintNFT<'info> {
        #[account(mut)]
        pub program: : Program<'info, Token>,
    }
    ```