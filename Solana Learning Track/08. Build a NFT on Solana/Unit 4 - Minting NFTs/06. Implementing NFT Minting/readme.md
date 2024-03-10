# Content/**Executing the `token::mint_to` Function**

After the previous lessons, where we configured and encapsulated the necessary programs and accounts for token minting, we're now ready to implement the minting of NFTs on Solana.

> We'll use the `token::mint_to` function provided by the Anchor framework to mint new NFTs. This function is a wrapper for Solana's Token Program, used to create new tokens.
> 

**Calling** `token::mint_to`**：**

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

		let cpi_program = ctx.accounts.token_program.to_account_info();
		let cpi_ctx = CpiContext::new(cpi_program, cpi_accounts);
		token::mint_to(cpi_ctx, 1)?;
}
```

**Analysis:**

- This function is responsible for creating a specified number of tokens in the designated ***mint*** account. In our case, we're minting `1` token, which is our new NFT.
- `cpi_ctx`： Encapsulates information like the mint account, the recipient account, and the authority account.

With this, we've successfully minted our NFT. But this is just the beginning. The NFT we minted is no different from a regular SPL token. A complete and unique NFT needs additional details like creator info, name, and image.

Starting from the next lesson, we'll learn how to add metadata to our freshly minted NFT.

**Syntax** 

function call

- hint
    
    ```rust
    pub fn my_function(ctx: Context<MyContext>) -> Result<()> {
        token::mint_to(cpi_ctx, amount)?;
    }
    ```