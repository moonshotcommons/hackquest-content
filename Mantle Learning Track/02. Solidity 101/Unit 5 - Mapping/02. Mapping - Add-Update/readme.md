# Content/Content

### Concept

For mappings, we could have adding, updating, deleting, and querying. We will talk about adding and updating in this part.

There is no fundamental difference between adding and modifying; both simply involve changing the value associated with a key in storage.

- Metaphor
    
    For example, if someone opened a new account in your bank and put in 10 dollars, then you want to add this new association to your balance mapping. 
    
- Real Use Case
    
    In the ***[_update](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/8186c07a83c09046c6fbaa90a035ee47e4d7d785/contracts/token/ERC20/ERC20.sol#L255)*** function of ERC20, modifications were made to the ***_balances*** mapping. The balance corresponding to ***from*** was updated to '***fromBalance*** - ***value***'.
    
    ```solidity
    function _update(address from, address to, uint256 value) internal virtual {
        _balances[from] = fromBalance - value;
    }
    ```
    

### Documentation

```solidity
mapping(address => uint256) public balance;
...
balance[address(0x123)] = 10; //this assigned a new value to address 0x123
balance[address(0x123)] = 20; //this updated the value from 10 to 20
```

Following the syntax to add and update a mapping

- balance - The name of the mapping variable
- address(0x123) - The key you want to add / update
- 10 - The value you want to associate with this key
- 20 - The new value you want to associate with this key

### FAQ

# Example/Example

```solidity
pragma solidity ^0.8.4;
contract book {
  //mapping(keyType => valueType) scope mappingName;
  mapping(address => uint) private owned_book;

  function add_book(uint bookID) public {
    //this will find the book given the owner
    owned_book[address(0x123)] = bookID;
  }
}
```
