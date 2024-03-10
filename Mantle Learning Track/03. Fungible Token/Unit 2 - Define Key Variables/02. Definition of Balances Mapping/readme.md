# Content/Definition of Balances Mapping

To track token balances efficiently, we use a mapping data structure. It associates *addresses* (token owners) with *unsigned integers* (token balances). 

Mapping 

1. offers fast lookup with unique keys
    
    Given any address, we could find the balance using syntax `balances[address]`.
    
2. allows dynamic addition and deletion of key-value pairs for convenient token transfers
    
    Again, we need to use `balances[address]=value` to add or delete a new pair.
    

**Syntax**

value types, mapping

- Hint
    
    ```solidity
    mapping (address => uint256) private balances;
    ```
    
