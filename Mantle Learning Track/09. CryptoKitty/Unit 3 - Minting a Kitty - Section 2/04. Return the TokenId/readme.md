# Content/Return the TokenId

So far, we have completed the creation of the kitty. Specifically, we have created the kitty’s information, associated the kitty's information with its TokenId, and minted the NFT.

Finally, we just need to increment the TokenId counter to point to the next TokenId to be minted then return the counter.

> If the caller wants to check the newly minted Kitty, they could use *_tokenIdCounter - 1 *****for Token ID
> 

**Syntax**

return

- hint
    
    ```solidity
    //In this example, we are still returning TokenId as 1, and completed the increment of TokenId
    TokenId = 1；
    return TokenId++;
    ```
    
