# Content/**Defining the `rent` Attribute**

In this lesson, we're going to explore the ***rent*** attribute in the ***MintNFT*** struct. This attribute is responsible for managing the Solana network's rent system account, which handles the account maintenance fees.

**Understanding the Concept of ‘Rent’ in Solana’s Account Model:**

1. Rent is different from transaction fees. Rent is paid to store data on the Solana blockchain, whereas transaction fees are paid for processing instructions on the network.
2. Unlike Ethereum, Solana charges for storing the state of an account on its network, referred to as rent. Rent is charged periodically based on the amount of token balance stored in an account. If an account fails to pay its rent, the system will remove it to save on storage costs for data that are no longer maintained. An account with assets exceeding the minimum balance for two years' rent can be exempt from paying rent.

**Adding the *rent* Attribute:**

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
		pub rent: AccountInfo<'info>,
}
```

**Syntax** 

macro struct

- hint
    
    ```rust
    #[derive(Accounts)]
    pub struct MintNFT<'info> {
        #[account(mut)]
        pub rent_account: AccountInfo<'info>,
    }
    ```