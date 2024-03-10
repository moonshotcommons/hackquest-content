# Content/Parameter Check

In the previous step, we defined a *function* with input *parameters*. Now it's time to consider whether the *function* needs to check the input *parameters*.

The input parameter here is the TokenId of the NFT, and we should ensure that the ***_TokenId*** value is within the range of the NFTs we have minted, which means ***_TokenId*** must be greater than *1* but less than ***nextTokenId***.

If an "out of range" ***_TokenId*** is passed to the query, it may cause an exception in the subsequent query process. Therefore, *parameter* checking here is very necessary.

**Syntax**

require

- hint
    
    ```solidity
    require(i > 1, "error");
    ```
    
