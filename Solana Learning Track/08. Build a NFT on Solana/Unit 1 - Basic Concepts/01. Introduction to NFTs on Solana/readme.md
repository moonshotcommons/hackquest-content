# Content/**Introduction**

**NFTs**

NFTs (Non-Fungible Tokens) represent a unique form of digital assets based on blockchain technology. Unlike fungible tokens, every NFT is distinct, making them an ideal medium for issuing digital art, collectibles, and gaming items.

**Solana NFTs**

While Ethereum has dedicated standards for NFTs such as **ERC-721** and **ERC-1155**, Solana's approach to NFTs relies on its SPL Token standard, with specific adaptations to accommodate the unique nature of NFTs.

This means that NFTs on Solana are implemented using the SPL Token standard, similar to other tokens, but with key differences:

- **Supply**: Each NFT has a supply of 1, ensuring its uniqueness.
- **Decimals**: NFTs have a decimal setting of 0, indicating they are indivisible.
    
    > Decimals refer to the number of digits after the decimal point. For example, a token with 2 decimals has a minimum unit of 0.01. A decimal setting of 0 means the minimum unit is 1, with no fractional part, hence indivisible.
    > 
- **Minting Authority**: **Minting** **Authority** is set to `null`, meaning that once minted, no new tokens of the same type can be created, ensuring a fixed supply and preserving uniqueness.

With this understanding, we see that an NFT on Solana is essentially a token with a supply of 1. But what is this NFT called? Where is its image stored? We don't know yet. Starting from the next lesson, we'll explore the **Metaplex** system, which provides a specialized protocol for NFTs, allowing us to add metadata to the token.

Stay tuned for more learning! 🚀🚀🚀