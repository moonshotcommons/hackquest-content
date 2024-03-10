# Content/Define the transfer function

Let's start defining the function header for the ***transfer*** *function*. In order to complete the ***transfer***, theoretically we need to know three *parameters*: the sender, the receiver, and the TokenId to be transferred. However, since you’re not supposed to transfer other’s NFT, we can use the `msg.sender` syntax to obtain the sender.

Therefore, here we only need two *parameters*: the receiver and the TokenId to be transferred.

Regarding the *visibility* selection, we chose `public` so it can be called everywhere.

This *function* does not need to return any information, so it has no *return* value.

**Syntax**

function, scope, msg.sender

- hint
    
    ```solidity
    //here we transfer the apple with specified appleId to the recipient.
    function transferApples(address recipient, uint256 appleId) public {
    
    }
    ```
    
