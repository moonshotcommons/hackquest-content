# Content/Obtaining NFT Information

After completing the *parameter* check, we can retrieve the NFT by TokenId using the ***tokens*** *mapping*, which provides us with a very convenient way to query.

Since we need to change the information of this **NFT** in the subsequent steps, we need to save the retrieved NFT in `storage`.

> If it exists in `memory`, the subsequent modifications will only exist in *memory* and will not be recorded after the completion of this *function*.
> 

**Syntax**

mapping

variable

- hint
    
    ```solidity
    NFT storage nft = NFTs[TokenId];
    ```
    
