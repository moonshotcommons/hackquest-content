# Content/Get the Sender's Wallet Address

Before deleting, we need to obtain the wallet and store it in `storage` for later modification operations.

> If it exists in `memory`, the subsequent modifications will only exist in *memory* and will not modify the state of the *contract*.
> 

Therefore, we need to use the *parameter **account*** to obtain the `uint256 array` of the wallet in the ***ownerTokens*** *mapping* here.

**Syntax Review**

array, data location

- hint
    
    ```solidity
    uint256[] storage arr = ownerTokens[account];
    ```