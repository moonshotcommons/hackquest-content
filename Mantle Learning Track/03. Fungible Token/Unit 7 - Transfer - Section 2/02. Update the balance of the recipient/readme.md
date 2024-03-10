# Content/Update the balance of the recipient

Since in the previous step we only updated the balance of the sender, we also need to update the balance of the recipient.

The action is opposite, where we need to add the **transfer** amount to the recipient's balance.

**Syntax Review**

mapping,variable

- hint
    
    ```solidity
    //Update balances
    balances[to] += amount;
    ```
    
