# Content/**Defining the `token_metadata_program` Attribute**

In this lesson, we will incorporate the ***token_metadata_program*** attribute into our ***MintNFT*** struct. This attribute points to a program that handles metadata, and since our project is developed using the **Metaplex** protocol (which we'll explore in more detail in later lessons), ***token_metadata_program*** refers to a **Metaplex** metadata program.

**Adding the *token_metadata_program* Attribute:**

```rust
#[derive(Accounts)]
pub struct MintNFT<'info> {
    #[account(mut)]
    pub mint_authority: Signer<'info>,
    #[account(mut)]
    pub mint: UncheckedAccount<'info>,
    pub token_program: Program<'info, Token>,
    #[account(mut)]
    pub metadata: UncheckedAccount<'info>,
    #[account(mut)]
    pub token_account: UncheckedAccount<'info>,
		pub token_metadata_program: UncheckedAccount<'info>,
}
```

> This program is responsible for managing and storing all metadata related to the NFT, such as descriptions, artist information, etc.
> 

**Syntax** 

macro struct

- hint
    
    ```rust
    #[derive(Accounts)]
    pub struct MintNFT<'info> {
        #[account(mut)]
        pub metadata_program: UncheckedAccount<'info>,
    }
    ```