# Content/Access Control

As we mentioned in the *parameter* check section, this *function* needs to implement access control to restrict the caller to be the owner of the NFT. We temporarily put this on hold because we couldn't obtain the owner's information.

Now that we have obtained the NFT information, we also know the caller of the *function*. It's time to implement access control!

**Syntax Review**

variable

- hint
    
    ```solidity
    require(owner != msg.sender, "error");
    ```
    
