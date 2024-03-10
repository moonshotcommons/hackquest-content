# Content/Add new NFT to tokens

Next, we need to inform our NFT tracking system (***tokens***) about the new NFT we just minted.

By “inform”, we just mean that we add this newly created NFT to the mapping, using its TokenId as an index. 

**Syntax Review**

mapping

- hint
    
    ```solidity
    books[bookidpointer] = newone;
    ```
    