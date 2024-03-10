# Content/**Implementing the Creation of `cpi_program`**

In this lesson, we're diving into how to obtain the ***cpi_program*** within the ***mint_nft*** function. 🌐 This is a key element in making Cross-Program Invocation (CPI) happen.

**What is a *cpi_program*?**

> The ***cpi_program*** represents the external program we need to call. In our NFT minting scenario, it refers to Solana's **Token Program**, responsible for handling operations related to token minting.
> 

> The **Token Program** is a core program in the Solana ecosystem, offering standard interfaces and methods for creating and managing tokens, including SPL tokens (Solana Program Library tokens). This program handles token issuance, transfers, minting, and more.
> 

**Defining the** ***mint_nft*** **function:**

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
}
```

- `ctx.accounts.token_program`： This is the Token Program's reference passed through the Anchor framework ***Context*** (***MintNFT***), specifically ***token_account***.
- `.to_account_info()` **：**Converts the Anchor-wrapped account ***token_account*** into Solana's native `AccountInfo` type.
- `AccountInfo`: It is the fundamental account type used in interactions between Solana programs. For cross-program calls, we need to convert to this basic type.
    
    

By converting the ***token_account*** (Token Program) into `AccountInfo` and assigning it to ***cpi_program***, we set the stage for interacting with the **Token Program** in the ***mint_nft*** function. This enables key operations like minting tokens, which we'll start exploring in the next lesson.

**Syntax** 

struct

- hint
    
    ```rust
    pub fn my_function(ctx: Context<MyContext>) -> Result<()> {
        let cpi_program = ctx.accounts.my_external_program.to_account_info();
    }
    ```