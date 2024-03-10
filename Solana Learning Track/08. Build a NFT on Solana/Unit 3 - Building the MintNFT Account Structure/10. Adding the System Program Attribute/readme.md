# Content/**Defining the `system_program` Attribute**

In this lesson, we'll focus on the ***system_program*** attribute within the ***MintNFT*** struct. It's primarily responsible for creating all accounts.

**Adding the *system_program* Attribute:**

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
		#[account(mut)]
    pub payer: AccountInfo<'info>,
		pub system_program: Program<'info, System>,
}
```

- `Program<'info, System>`： The ***system_program*** uses the `Program` type and refers to Solana's System Program. This system program is a fundamental component of Solana , providing basic functionalities like account creation, management, and fund transfers.

In our project, defining ***system_program*** allows us to leverage these basic functionalities for account creation and modification.

**Syntax** 

macro struct

- hint
    
    ```rust
    #[derive(Accounts)]
    pub struct MintNFT<'info> {
        #[account(mut)]
        pub system: AccountInfo<'info>,
    }
    ```