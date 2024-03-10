# Content/Define owner address

We have defined two *variables*, ***balances*** and ***totalSupply***, completing the basic structure of the token. 

However, access control is crucial in currency systems. For example, the US dollar is controlled by the Federal Reserve System to prevent misuse. If everyone can make their own US dollars at will, the entire economic system will collapse.

Similarly, in our token *contract*, an "administrator" is needed to control token minting and circulation. 

To enable access control, we use an address variable to represent the token issuer's identity.

**Syntax**

value types

- Hint
    
    ```solidity
    contract Example{
      address private a;
    }
    ```
    
