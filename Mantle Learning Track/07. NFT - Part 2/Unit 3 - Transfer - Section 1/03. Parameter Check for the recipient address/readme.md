# Content/Parameter Check for the recipient address

After defining the *function header*, we need to consider whether this *function* has any *parameter* restrictions and access control.

Since this is a ***transfer*** *function* called by the caller, we need to ensure that the caller is the owner of the NFT. However, since we cannot currently obtain the owner of the NFT that has been transferred, we will temporarily postpone this matter.

In terms of *parameter* restrictions, it is obvious that since this *function* is a transfer *function*, the address we are transferring to must be a *non-zero* *address*. This is to prevent users from making mistakes and transferring NFTs to *zero addresses*, resulting in the loss of NFTs.

> 0 address is an *address* with no owner, so any asset transferred to this *address* is lost.
> 

**Syntax**

require, address

- hint
    
    ```solidity
    require(amount <= balances[msg.sender]);
    ```
    
