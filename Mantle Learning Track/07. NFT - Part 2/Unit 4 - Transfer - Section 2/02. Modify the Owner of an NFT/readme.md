# Content/Modify the Owner of an NFT

So far, we have completed *parameter* checking and access control, and have obtained the *storage variables* of the **NFT** that will be transferred, ***token***.

Now, what we need to do is to modify the owner information of the NFT.

**Syntax Review**

variable

- hint
    
    ```solidity
    //Update owner information
    NFT.owner = recipient;
    ```
    
