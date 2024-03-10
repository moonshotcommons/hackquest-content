# Content/Define the balanceOf Function

Earlier, we mentioned that this function **is used to query the balance. To do that, we need an input parameter that represents the account address to be queried.

To indicate that the *function* would not modify the *contract's* state and does not consume gas, we decorate it with the `view` state mutability.

> In other words, it is read-only *function* that only retrieves and returns information from the *contract* without making any changes to the data.
> 

In terms of *function* visibility, we choose to use `public` to ensure the *function* is accessible for balance checking both inside and outside the *contract*.

Since we are checking the balance, we need to return the balance as the *function's* `return` value. As mentioned before, the balance is always non-negative, so we use `uint256` as the *return* type.

**Syntax**

view,return,scope,function

- hint
    
    ```solidity
    //for example, here we define a function that can return a non-negative integer
    function getData() public view returns(uint256){
      return 5;
    }
    ```
    
