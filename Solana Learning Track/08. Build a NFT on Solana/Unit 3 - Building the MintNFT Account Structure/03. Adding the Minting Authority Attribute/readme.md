# Content/**Defining the `mint_authority` Attribute**

In this lesson, we're going to start fleshing out the attributes of our ***MintNFT*** struct.

First up, we're defining the ***mint_authority*** attribute. This attribute is in charge of the authorization and signing of transactions. In simple terms, it defines who has permission to initiate the NFT minting operation.

**Adding the *mint_authority* Field:**

```rust
#[derive(Accounts)]
pub struct MintNFT<'info> {
    #[account(mut)]
    pub mint_authority: Signer<'info>,
}
```

- `Signer<'info>`：***mint_authority*** is of the `Signer` type. This represents the account that will perform the NFT minting operation, supporting transaction and signing functionalities.
- `#[account(mut)]`：This attribute macro indicates that ***mint_authority*** is a mutable account reference. Since the state of this account (like balance) might change during the minting process, we need to mark this attribute as `mutable`.

**Syntax** 

macro struct

- hint
    
    ```rust
    #[derive(Accounts)]
    pub struct MintNFT<'info> {
    		#[account(mut)]
        pub authority: Signer<'info>,
    }
    ```