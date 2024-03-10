# Content/Access control

After retrieving the information for the kitty’s mom and dad, we need to impose some controls because we can't allow just any two cats to **breed**, or else the kitties would not have any value!

To ensure this, we'll require that the caller of this function is the owner of both the mom and dad kitties.

To determine the ownership of the mom and dad, we can directly use the ***ownerOf*** function from the ERC721 standard, passing in the respective TokenId as a parameter.

**Syntax**

require

- hint
    
    ```solidity
    require(owner == msg.sender, "error");
    ```
    
