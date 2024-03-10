# Content/Removing NFT from sender's wallet

After modifying the owner of the **NFT**, we need to update the wallet information of both the sender and the receiver.

So, let's start by modifying the sender's wallet. What we need to do is to remove the TokenId of this **NFT** from the sender's wallet ***ownerTokens***.

Here, we only need to call this ***deleteById*** *function*, which requires two *parameters* for the query: the owner of the wallet to be deleted and the TokenId of the **NFT** to be deleted.

**Syntax Review**

variable

- hint
    
    ```solidity
    //Call the delete function
    deleteById(msg.sender, id);
    ```
    
