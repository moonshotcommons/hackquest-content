# Content/Updating the mint function

Since we have just added a new *mapping* "***ownerTokens***" to query all NFTs owned by a specific *address*, we need to make some changes to the ***mint*** *function*. We need to first find the caller’s wallet, and then use the `push` statement to add the tokenId to the array.

**Syntax Review**

array

- hint
    
    ```solidity
    //For example, here we are adding element a to the end of the arr array
    arr.push(a);
    ```
    
