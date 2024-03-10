# Content/Update Balances

After implementing access control, we can finally start **minting** the token.

In *smart contract*, **minting** tokens is simply updating *variables*.

Just like in real life, the balance we see on our mobile banking app represents the money we own. Similarly, in the world of blockchain, we only need to maintain a variable that represents our balance.

Here, we can achieve token **minting** by adding the **minted** amount to the balance recorded in ***balances***.

Firstly, let’s update the balance recorded in ***balances***. We should add the amount of tokens **minted** to the account of recipient.

**Syntax Review**

value types

- Hint
    
    ```solidity
    //update balances
    balances[to] += amount;
    ```
    
