# Content/**Creating the `cpi_accounts` Instance**

In this lesson, we're going to tackle how to create and assign the ***cpi_accounts*** within the ***mint_nft*** function. 🛠️ This includes all the necessary account information for our NFT minting operations - essential stuff for our NFT creation.

**What is CPI?**

> **CPI** stands for "**Cross-Program Invocation**" in Solana programming and the Anchor framework. It's a way for Solana smart contracts (programs) to interact with each other, allowing one program (contract) to call functions or methods of another program already deployed on Solana.
> 

> It's used in various scenarios like handling token transactions, reading and writing data to the blockchain, or interacting with other smart contracts.
> 

> For example, in NFT minting, a program needs to call the Solana Token Program to create a new token or modify its state. This is done through CPI - one program (NFT minting program) calling the functions of another (Token Program).
> 

**Creating the** ***cpi_accounts*** **instance within the function:**

```rust
pub fn mint_nft(
        ctx: Context<MintNFT>,
        creator_key: Pubkey,
        uri: String,
        title: String) -> Result<()> {
        
				let cpi_accounts = MintTo {
        mint: ctx.accounts.mint.to_account_info(),
        to: ctx.accounts.token_account.to_account_info(),
        authority: ctx.accounts.payer.to_account_info(),
    };
}
```

`cpi_accounts` **：** It's an instance of the ***MintTo*** struct, containing the account info needed for NFT minting operations, and prepping for cross-program calls.

- ***mint***： Points to the NFT's mint account for minting the NFT.
- ***to***： The target account to receive the minted NFT.
- ***authority***： The authorized account executing the minting, usually the one paying the transaction fees.

With this, we've set up the essential account info for NFT minting. In our next class, we'll explore another key piece for minting operations - the **Token Minting Program**.

**Syntax** 

struct

- hint
    
    ```rust
    pub fn my_function(ctx: Context<MyContext>) -> Result<()> {
        let cpi_accounts = MyCpiStruct {
            account_one: ctx.accounts.account_one.to_account_info(),
            account_two: ctx.accounts.account_two.to_account_info(),
        };
    }
    ```