# Content/Define the creatKittyGen0 function

First, let’s draft the header of the function named ***createKittyGen0***.

This function requires no inputs since we're creating a kitty from scratch. It will be `private` to ensure that only our contract can generate a kitty in this manner.

Upon successful creation, we will return the next available Token ID to inform the caller of the successful operation.

**Syntax**

function

scope

return

- hint
    
    ```solidity
    function create() public returns (uint256) {
    ```
    
