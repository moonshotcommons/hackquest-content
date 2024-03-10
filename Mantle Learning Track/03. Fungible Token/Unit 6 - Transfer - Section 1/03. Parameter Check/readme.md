# Content/Parameter Check

In the previous step, we defined the ***transfer*** function. Now it's time to consider whether the *function* needs to check the input *parameters*.

Obviously, we do not want users to be able to **transfer** more tokens than they have.

Therefore, we need to check the input parameter ***amount*** to ensure that it is not greater than the balance, which stored in the caller's corresponding ***balances*** *mapping*.

We should also check the **transfer** amount is greater than *0* otherwise the user could steal money from others! However, we don’t need to explicitly check it because ***amount*** is in the type of `uint256`, which could only be positive. 

**Syntax**

require,mapping,msg.sender

- hint
    
    ```solidity
    require(amount <= balances[msg.sender]);
    ```
    
