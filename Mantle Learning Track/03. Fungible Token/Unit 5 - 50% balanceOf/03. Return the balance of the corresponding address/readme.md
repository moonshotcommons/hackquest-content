# Content/Return the balance of the corresponding address

After defining the *function*, it's time to implement it.

Firstly, in order to return the balance of the specified address, we will look up the balance corresponding to that *address* from the ***balances*** *mapping*.

Then, `return` that balance as the *function* *return* value.

**Syntax**

return,mapping

- hint
    
    ```solidity
    //For example, here we define a function that can return an integer "5"
    function getData() public view returns(uint256){
      return map[index];
    }
    ```
    
