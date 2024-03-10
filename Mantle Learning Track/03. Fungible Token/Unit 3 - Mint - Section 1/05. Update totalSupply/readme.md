# Content/Update totalSupply

We updated the ***balances*** in previous step, so the recipient has more tokens in their account.

Think about it, since we have **minted** new tokens, shouldn't we also update the total amount of tokens issued, which is recorded in ***totalSupply***?

To reflect the newly minted tokens, we need to add the **minted amount** to ***totalSupply***.

**Syntax Review**

value types

- Hint
    
    ```solidity
    total += amount;
    ```
    
