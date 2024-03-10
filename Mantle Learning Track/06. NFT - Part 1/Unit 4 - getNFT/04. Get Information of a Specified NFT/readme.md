# Content/Get Information of a Specified NFT

After completing the checks for *parameters*, we can now proceed with the actual query.

Do you remember the ***tokens*** that we defined earlier? It is used to store the one-way lookup relationship of TokenId to NFT detailed information.

So, we need to query the detailed information of the NFT corresponding to the input TokenId from the ***tokens***.

We will store the detailed information of this NFT in the `memory` of this function for *returning* the information in subsequent operations.

> The reason for choosing `memory` is that storing data in *memory* is more cost-effective in terms of gas fees. Therefore, we generally use `memory` to store temporary data.
> 

**Syntax**

mapping, data location

- hint
    
    ```solidity
    Token memory token = tokens[id];
    ```
    
