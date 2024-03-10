# Content/Remove the TokenId from the owner's wallet

Now, we begin the deletion process~

Firstly, we need to remove the **NFT** from the owner's wallet. Do you still remember the ***deleteById** function* we defined to achieve this?

It's time to use it! Let's directly call the *function* with the `msg.sender` and ***_tokenId*** as *parameters*.

**Syntax Review**

variable

- hint
    
    ```solidity
    //Call the delete function
    deleteById(msg.sender, id);
    ```
    
