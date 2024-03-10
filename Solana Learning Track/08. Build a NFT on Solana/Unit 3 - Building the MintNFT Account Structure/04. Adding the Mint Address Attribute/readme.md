# Content/**Defining the `mint` Attribute**

This lesson continues our journey in enhancing the ***MintNFT*** struct, and now we're going to define the ***mint*** field, which is crucial for creating new NFTs.

On Solana, every NFT is associated with a unique ***mint*** account. The address of this account is what identifies the NFT, ensuring its uniqueness.

**Adding the *mint* Field:**

```rust
#[derive(Accounts)]
pub struct MintNFT<'info> {
    #[account(mut)]
    pub mint_authority: Signer<'info>,
    #[account(mut)]
    pub mint: UncheckedAccount<'info>,
}
```

- `#[account(mut)]`： This attribute macro indicates that ***mint*** is a mutable account reference. During the NFT minting process, the state of the ***mint*** account may change (as a new NFT is added), hence it's marked as mutable.
- `UncheckedAccount` VS. `Account`
    
    The ***mint*** attribute uses `UncheckedAccount` as its account type instead of `Account` because:
    
    1. When you use the `Account` type, the Anchor framework automatically performs a series of checks and validations, like verifying account ownership and ensuring it's not closed.
    2.  In NFT minting scenarios, using `UncheckedAccount` allows for custom validations and error handling, offering more control and flexibility in operations.

**Syntax** 

macro struct

- hint
    
    ```rust
    #[derive(Accounts)]
    pub struct MintNFT<'info> {
        #[account(mut)]
        pub myAccount: UncheckedAccount<'info>,
    }
    ```