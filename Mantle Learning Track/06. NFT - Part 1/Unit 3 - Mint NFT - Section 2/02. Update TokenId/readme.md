# Content/Update TokenId

You’ve noticed that we used ***nextTokenId*** to be the index of the newly created NFT. 

Since TokenId has been used already, we need to increment it by *1* so we can assign the right value to our NFT next time. 

**Syntax Review**

mapping, struct

- hint
    
    ```solidity
    bookidpointer++;
    ```
    