# Content/Updating the balance of the transferrer

After checking the *parameters*, we need to implement the ***transfer*** function.

In the ***transfer*** process, there are actually two changes in the balance, one is the balance of the transferor and the other is the balance of the recipient.

When writing the ***transfer*** code, a good habit is to write it according to the logical order of the **transfer**, subtracting first and adding later. 

So here, we first subtract the ******amount from the balance of the transferrer.

**Syntax**

mapping,variable

- hint
    
    ```solidity
    //Update balances.
    //Here, the syntax using "-=" is equivalent to "balances[from] = balances[from] - amount;".
    //But this way makes the code more concise.
    balances[from] -= amount;
    ```
    
