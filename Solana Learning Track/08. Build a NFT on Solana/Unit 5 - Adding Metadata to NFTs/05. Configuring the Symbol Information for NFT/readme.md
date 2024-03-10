# Content/**Setting Up the Symbol**

In this lesson, we will learn how to configure symbol information related to an NFT, which is used to represent the NFT's symbol, similar to "**AZUKI**" or Bored Ape Yacht Club's "**BAYC**".

**Defining the *symbol* Attribute:**

The ***symbol*** string in NFT metadata serves as a shorthand identifier for the token. It's akin to the token symbols in cryptocurrency or stock tickers in the stock market.

```rust
pub fn mint_nft(
        ctx: Context<MintNFT>,
        creator_key: Pubkey,
        uri: String,
        title: String) -> Result<()> {
        
		// ... previous code ...
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

		let symbol = std::string::ToString::to_string("nft_symb");
}
```

In this example, we use *nft_symb* as the symbol for our NFT project, representing our NFT collection.

By defining the ***symbol*** attribute, we can assign a clear, recognizable identifier to our NFT during creation. This is very helpful for categorizing and identifying NFTs. With the account, creator, and NFT symbol information set, our next lesson will be about creating metadata accounts.

**Syntax** 

string

- hint
    
    ```rust
    let symbol = std::string::ToString::to_string("my_symbol");
    ```
    