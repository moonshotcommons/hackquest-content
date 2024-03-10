# Content/Define _tokenIdCounter

We've set up our CryptoKitty *contract* using ERC721 and will define a `public uint256` variable, ***_tokenIdCounter***, to track minted (including the ones we’ve burnt) NFTs. 

It's needed for the ***_mint*** function in ERC721, which requires unique TokenIDs for each NFT. 

> You may want to check out the ***_mint** function* in ERC721 *contract*. It’s similar to the mint we’ve written in our own NFT project.
> 

We initialize ***_tokenIdCounter*** to *1* so that NFT TokenIds start from this value.

> *_tokenIdCounter* - *1* is the number of NFTs we’ve minted.
> 

**Syntax**

interface

- hint
    
    ```solidity
    uint256 public TokenId;
    ```
    
