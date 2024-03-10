# Content/**Defining the `metadata` Attribute**

In this lesson, we're going to enrich our ***MintNFT*** struct by adding the ***metadata*** attribute. This attribute will be used to store and reference metadata related to the NFT.

**Adding the *metadata* Attribute:**

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
}
```

- `#[account(mut)]` ： This signifies that ***metadata*** is a mutable account reference. During the NFT minting process, the state of this account (like the stored information) might change.

**Syntax** 

macro struct

- hint
    
    ```rust
    #[derive(Accounts)]
    pub struct MintNFT<'info> {
        pub data: UncheckedAccount<'info>,
    }
    ```