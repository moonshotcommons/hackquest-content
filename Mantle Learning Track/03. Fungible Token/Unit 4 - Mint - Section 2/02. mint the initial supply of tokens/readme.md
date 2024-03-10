# Content/Mint the initial supply of tokens to the deployer

Now, let's **mint** the initial supply of tokens to the issuer at the time of deployment.

The constructor is automatically executed when the *contract* is deployed, so we choose to call the ***mint*** *function* within the *constructor*.

**Syntax**

function call

- Hint
    
    ```solidity
    constructor(int a){
      mint(msg.sender, a)
    }
    ```
    
