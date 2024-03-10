# Content/**Setting Up Creator Information**

In this lesson, we will learn how to create an array of creator information related to an NFT. This array is used to store information about the creators of the NFT and is a crucial part of defining its metadata.

**Creating the *creator_arr* Array:**

In the metadata of an NFT, the ***creator_arr*** array records the creator information. This data is vital for tracking the origins and copyrights of the NFT.

```rust
pub fn mint_nft(
        ctx: Context<MintNFT>,
        creator_key: Pubkey,
        uri: String,
        title: String) -> Result<()> {
        
		// ... previous code ...

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

		let creator_arr = vec![
            mpl_token_metadata::state::Creator {
                address: creator_key,
                verified: false,
                share: 100,
            },
            mpl_token_metadata::state::Creator {
                address: ctx.accounts.mint_authority.key(),
                verified: false,
                share: 0,
            },
     ];
}
```

***Creator* Attributes Explained:**

- Each ***Creator*** structure represents a creator, including their address, verification status, and royalty percentage.
- ***address***: The creator's address.
- ***verified***: Indicates whether the creator's identity has been confirmed and verified. In the NFT market, this can enhance the NFT's credibility. Initially set to *false* in this example.
- ***share***: The percentage of royalties attributed to the creator.

We define **two** creators:

1. **The primary creator**: ***address*** field set to ***creator_key***, representing the NFT's original creator. `share: 100` indicates the original creator owns 100% of the related royalties.
2. **The assisting creator**: someone authorized to help with creation, with the ***address*** set to ***ctx.accounts.mint_authority.key()***, indicating they are the NFT's minting authority. `share: 0` means they have no share in royalties, typically a helper role or collaborator.

This multi-role setup gives our NFT creation a more authentic feel, showing each member's role in the creative team and their different royalty incomes. Having set up the creator information, our next lesson will explore symbol information related to NFT metadata.

**Syntax** 

array

- hint
    
    ```rust
    let creators = vec![
            Creator {
                address: my_creator_key,
                verified: false,
                share: 100,
            },
            // ... 可能的其他创作者 ...
        ];
    ```
    