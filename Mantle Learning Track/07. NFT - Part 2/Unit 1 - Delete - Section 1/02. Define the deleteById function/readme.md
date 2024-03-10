# Content/Define the deleteById function

Firstly, we need to define the header of the ***deleteById*** *function*.

As this *function* needs to delete a certain TokenId from the wallet of a specified address, we need two input *parameters*, namely the *address* of the account (who’s wallet) and the TokenId (which NFT).

In terms of the *function's* *visibility*, since we do not want anyone to be able to call this *function* as it can delete anyone's NFT, we define it as an `internal` *function*, which can only be called by other *functions* **within** the *contract*.

**Syntax Review**

variable

- hint
    
    ```solidity
    function deletefunction(address addr, uint256 TokenId) internal { }
    ```
    
