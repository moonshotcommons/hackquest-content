# Content/Content

### Concept

Deleting refers to the removal of a **key-value** pair from a *mapping*, effectively erasing the association between a key and its corresponding value.

<aside>
💡 Deleting is essentially just resetting the value associated with the key to its default value.

</aside>

- Metaphor
    
    Sometimes, we want to remove the **key-value** pair. For example, if the account owner wants to close her account in your bank, you will need to give her all the money and delete the account.
    
- Real Use Case
    
    Using `delete` in the ***[cancel](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/governance/TimelockController.sol#L341)*** function of the ***TimelockController*** contract to remove the value associated with ***id*** in the ***timestamps*** mapping.
    
    ```solidity
    function cancel(bytes32 id) public virtual onlyRole(CANCELLER_ROLE) {
        ...
        delete _timestamps[id];
    }
    ```
    

### Documentation

```solidity
delete balance[address(0x123)];
```

To delete a **key-value** pair, we use the keyword `delete`. 

### FAQ

- What is the difference between deleting and assigning default values?
    
    Here deleting is actually the same as assigning the value to be the default *value*. In Solidity, if you try to query an **unsigned** key, it will *return* the default *value*. Returning the *default value* is not a universal behavior, as in other programming languages, it could report an error. 
    

# Example/Example

```solidity
pragma solidity ^0.8.4;
contract A {
  mapping(address => uint) public balance;

  function add() public {
    balance[address(0x0000000000000000000000000000000000000123)] = 10;
  }

  function deleteF() public {
    delete balance[address(0x0000000000000000000000000000000000000123)];
  }

  function update() public{
    balance[address(0x123)] += 10;
  }
}
```
