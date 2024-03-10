# Content/Authorization Control

After defining the function header, now we can implement the *function*.

First, let's consider that if everyone can obtain a thing at will, its value will be lost, therefore, currency has always been a scarce commodity. 

So, the ***mint*** *function* needs to have an access control over the caller. 

We will check if the caller's address is the issuer recorded as the ***owner***. If it is not, the call will fail.

**Syntax**

require, msg.sender

- Hint
    
    ```solidity
    require(msg.sender == owner,"not the owner");
    ```
    
