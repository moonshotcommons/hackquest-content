# Content/**Defining Account Information**

In this lesson, we're going to learn how to configure the array of accounts required for defining a **Master Edition**. This array includes all the account information necessary for storing and creating the Master Edition PDA related to the NFT.

**Defining the Account Array:**

```rust
pub fn mint_nft(
        ctx: Context<MintNFT>,
        creator_key: Pubkey,
        uri: String,
        title: String) -> Result<()> {
        
		// ... previous code ...

		let master_edition_infos = vec![
        ctx.accounts.master_edition.to_account_info(),
        ctx.accounts.mint.to_account_info(),
        ctx.accounts.mint_authority.to_account_info(),
        ctx.accounts.payer.to_account_info(),
        ctx.accounts.metadata.to_account_info(),
        ctx.accounts.token_metadata_program.to_account_info(),
        ctx.accounts.token_program.to_account_info(),
        ctx.accounts.system_program.to_account_info(),
        ctx.accounts.rent.to_account_info(),
    ];
}
```

Similar to the array needed for adding metadata, the account information required for creating a **Master Edition** includes accounts like ***master_edition***、***mint***、***mint_authority***、***payer***, etc. Each account is converted to Solana's ***AccountInfo*** type using the ***to_account_info*** method.

With this setup, we're prepared to add the Master Edition to our NFT. In the next lesson, we'll learn how to create the **Master Edition**.

**Syntax** 

array

- hint
    
    ```rust
    let account_info = vec![
            ctx.accounts.my_account_one.to_account_info(),
            ctx.accounts.my_account_two.to_account_info(),
    ];
    ```
    
