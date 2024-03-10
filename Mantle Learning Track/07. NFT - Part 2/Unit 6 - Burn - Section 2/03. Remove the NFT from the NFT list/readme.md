# Content/Remove the NFT from the NFT list

Now that we have deleted the information about the NFT in the wallet, there is still information in the ***_tokens*** *mapping* of the NFT list in the *contract* that needs to be deleted.

Deleting from *mapping* is simple, just use the `delete` statement.

**Syntax Review**

delete

mapping

- hint
    
    ```solidity
    delete map[key];
    ```
    