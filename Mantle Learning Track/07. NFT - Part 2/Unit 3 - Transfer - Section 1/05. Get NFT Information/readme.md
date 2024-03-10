# Content/Get NFT Information

After completing *parameter* checks, we can retrieve the NFT by TokenId using the ***tokens***, which provides a very convenient query method.

Because we need to modify the information of the retrieved NFT in the subsequent steps, we need to store it in `storage`.

**Syntax**

mapping, variable

- hint
    
    ```solidity
    NFT storage nft = NFTs[TokenId];
    ```
    
