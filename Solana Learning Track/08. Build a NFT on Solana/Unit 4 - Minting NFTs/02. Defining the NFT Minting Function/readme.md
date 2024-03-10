# Content/Defining the **`mint_nft` Function**

In this lesson, we're going to learn how to define the ***mint_nft*** function within the ***metaplex_nft*** module. 🌟 This is where we'll craft the core code for minting our NFTs.

**Defining the** ***mint_nft*** **function:**

```rust
#[program]
pub mod metaplex_anchor_nft {
    // ...do somethind...

    pub fn mint_nft(
        ctx: Context<MintNFT>,
        creator_key: Pubkey,
        uri: String,
        title: String,
    ) -> Result<()> {
        // implement...
    }
}
```

**Function Parameters:**

- `ctx: Context<MintNFT>`： A context containing all necessary account information for NFT minting operations.
- `creator_key: Pubkey`： The public key of the creator, representing the NFT's creator.
- `uri: String`： The **URI** for NFT metadata, usually a link to detailed information about the NFT.
- `title: String`： The title of the NFT.

 

Starting from our next lesson, we'll step by step complete the functional code of the ***mint_nft*** function. This includes creating a new NFT, setting its metadata, and managing its minting and issuance. 🚀

**Syntax** 

function

- hint
    
    ```rust
    pub fn my_function(ctx: Context<MyContext>) -> Result<()> {
        Ok(())
    }
    ```