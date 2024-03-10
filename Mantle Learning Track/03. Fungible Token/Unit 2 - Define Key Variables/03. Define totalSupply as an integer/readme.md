# Content/Define totalSupply as an integer

Now that we have the ***balances*** *mapping*, which represents the balance of each address, we still need a *variable* to represent the total amount of tokens that have been issued; we named it ***totalSupply***.

***TotalSupply*** allows the administrator to check and manage the total supply of tokens conveniently.

Regarding data type selection, we choose `uint256` for non-negative values and larger numerical representations. 

**Syntax**

value types

- Hint
    
    ```solidity
    contract Example{
      uint256 public totalSupply;
    }
    ```
    
