# Content/Restricting the owner in the constructor

Previously, we mentioned that the ***owner*** *variable* needs to be defined as the issuer of the token, which is the **deployer** of the contract.

The only way to determine the deployer in the *contract* is by using the `msg.sender` syntax in the constructor. 

> The *constructor* executes only once during *contract* deployment, and the deployer is the **default caller**.
> 

Therefore, we need to add one line of code to record the issuer of the token in the *constructor*.

**Syntax**

constructor, msg.sender

- Hint
    
    ```solidity
    constructor(int a, bool b){
      the_owner = msg.sender;
    }
    ```
    
