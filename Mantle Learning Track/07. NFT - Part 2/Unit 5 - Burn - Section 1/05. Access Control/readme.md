# Content/Access Control

As mentioned when defining the *function*, we need to implement access control to restrict callers to the owner of the **NFT**.

Now that we have obtained information about the **NFT**, we also know its owner. We can now proceed to implement access control!

**Syntax Review**

variable

- hint
    
    ```solidity
    require(owner != msg.sender, "error");
    ```
    
