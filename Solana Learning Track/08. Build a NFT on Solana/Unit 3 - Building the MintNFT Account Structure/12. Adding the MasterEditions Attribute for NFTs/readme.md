# Content/**Defining the `master_edition` Attribute**

In this lesson, we'll explore the ***master_edition*** attribute in the ***MintNFT*** struct. This attribute is crucial in the process of minting NFTs as it represents the NFT's '**Master Edition**,' which is responsible for managing the limited supply of NFTs and maintaining consistency in their metadata.

> In the Metaplex Solana NFT standard, the concept of **MasterEditions** refers to a '**master**' NFT where users specify the number of copies to be minted and provide metadata information to ensure its rarity and uniqueness. (We'll delve into this in more detail later.)
> 

**Adding the *master_edition* Attribute:**

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
		#[account(mut)]
    pub master_edition: UncheckedAccount<'info>,
}
```

**Syntax** 

macro struct

- hint
    
    ```rust
    #[derive(Accounts)]
    pub struct MintNFT<'info> {
        #[account(mut)]
        pub master_edition: UncheckedAccount<'info>,
    }
    ```