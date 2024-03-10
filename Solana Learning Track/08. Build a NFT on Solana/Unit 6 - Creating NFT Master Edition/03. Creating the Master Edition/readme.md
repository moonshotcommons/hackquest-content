# Content/Creating the Master Edition

Do you remember how we learned to import the `create_master_edition_v3` function earlier? It's a function in the **Metaplex** framework, used for creating the **Master Edition** of our NFT on the Solana blockchain.

> The `create_master_edition_v3` function creates the **Master Edition** of an NFT, which represents the original version of the NFT. It allows creators to produce a limited or unlimited number of copies (Prints), meaning this call can set the maximum number of versions minted, controlling the scarcity and uniqueness of the NFT.
> 

**Calling `create_master_edition_v3` ：**

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

		invoke(
        &create_master_edition_v3(
            ctx.accounts.token_metadata_program.key(),
            ctx.accounts.master_edition.key(),
            ctx.accounts.mint.key(),
            ctx.accounts.payer.key(),
            ctx.accounts.mint_authority.key(),
            ctx.accounts.metadata.key(),
            ctx.accounts.payer.key(),
            Some(0),
        ),
        master_edition_infos.as_slice(),
    )?;
}
```

- ***Some(0)***: Sets the maximum minting number. Here, *0* indicates no limit.

Executing this operation creates a **Master Edition** for our NFT on the blockchain, ensuring its status as the original version with the ability to manage copies.

With this, we have completed the entire minting process for our NFT, including minting the initial NFT account, adding metadata, and creating the **Master Edition** to manage the issuance. 🎉🎉

Next, let's dive into the interactive segment, creating and minting our own NFT!

**Syntax** 

function

- hint
    
    ```rust
    invoke(
            &create_my_metadata(
                // 参数...
            ),
            my_account_info.as_slice(),
    )?;
    ```
    
