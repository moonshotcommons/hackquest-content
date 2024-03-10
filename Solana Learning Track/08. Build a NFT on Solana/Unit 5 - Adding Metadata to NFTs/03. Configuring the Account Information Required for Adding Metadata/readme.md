# Content/Defining Account Information

In this lesson, we're going to learn how to configure the array of accounts needed for adding metadata. This array contains all the key account information necessary for minting NFTs and creating metadata, forming the basis for interaction with Metaplex's Token Metadata program.

**Defining the Account Array:**

```rust
pub fn mint_nft(
        ctx: Context<MintNFT>,
        creator_key: Pubkey,
        uri: String,
        title: String) -> Result<()> {
        
		// ... 前面的代码 ...

		let account_array = vec![
        ctx.accounts.metadata.to_account_info(),
        ctx.accounts.mint.to_account_info(),
        ctx.accounts.mint_authority.to_account_info(),
        ctx.accounts.payer.to_account_info(),
        ctx.accounts.token_metadata_program.to_account_info(),
        ctx.accounts.token_program.to_account_info(),
        ctx.accounts.system_program.to_account_info(),
        ctx.accounts.rent.to_account_info(),
    ];
}
```

- ***metadata***: Stores NFT metadata information such as name, description, image link, etc.
- ***mint***: The mint account for the NFT, identifying its uniqueness.
- ***mint_authority***: The minting authority account with the power to create the NFT.
- ***payer***: The account paying for transaction fees.
- ***token_metadata_program***: The account for Metaplex's Token Metadata program, used for creating and updating NFT metadata.
- ***token_program***: Solana's Token Program account for performing token-related operations.
- ***system_program***: Solana's system program account for basic program operations.
- ***rent***: Solana network's rent account, used to pay for data storage costs.

With these account details configured, we're set to add NFT metadata. In the next lesson, we'll continue exploring other configurations related to NFT metadata, like creator, name, description, and more.🚀✨

**Syntax** 

array

- hint
    
    ```rust
    let account_info = vec![
            ctx.accounts.my_account_one.to_account_info(),
            ctx.accounts.my_account_two.to_account_info(),
    ];
    ```
    