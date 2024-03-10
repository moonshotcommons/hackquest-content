# Content/**Defining the `payer` Attribute**

In this lesson, we're going to focus on the ***payer*** attribute within the ***MintNFT*** struct. This attribute plays a crucial role during the execution of our program, primarily responsible for paying transaction fees and handling other fund-related operations.

**Adding the *payer* Attribute:**

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
}
```

- We mark this account with the `#[account(mut)]` macro because the transaction fees involved will necessitate changing the account's balance.
- `AccountInfo<'info>`： The ***payer*** account uses Anchor's `AccountInfo` account type. The `Account` account type is generally safer for declaring accounts and includes all `AccountInfo` methods. However, it's best used when you need to check account ownership or deserialize data into a specific type.

**Syntax** 

macro struct

- hint
    
    ```rust
    #[derive(Accounts)]
    pub struct MintNFT<'info> {
        #[account(mut)]
        pub payer_account: AccountInfo<'info>,
    }
    ```