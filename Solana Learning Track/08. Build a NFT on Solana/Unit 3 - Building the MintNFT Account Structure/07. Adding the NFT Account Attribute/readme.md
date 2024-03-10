# Content/**Defining the `token_account` Attribute**

In this section, we're adding the ***token_account*** attribute to our ***MintNFT*** struct. This attribute represents the token account associated with the NFT that's about to be minted. Put simply, the program will send the newly minted NFT to the account specified by ***token_account***.

**Adding the *token_account* Attribute:**

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
}
```

**Syntax** 

macro struct

- hint
    
    ```rust
    #[derive(Accounts)]
    pub struct MintNFT<'info> {
        #[account(mut)]
        pub receive_account: UncheckedAccount<'info>,
    }
    ```