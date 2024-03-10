# Content/Content

### Concept

Querying a *mapping* in Solidity refers to accessing the value associated with a specific key (usually an address or identifier) within the *mapping data* structure to retrieve information or perform actions based on that value.

- Metaphor
    
    Querying in Solidity is like looking up a contact's phone number in a phone book to get their information and interact with them.
    
- Real Use Case
    
    Using the [***balanceOf***](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/8186c07a83c09046c6fbaa90a035ee47e4d7d785/contracts/token/ERC20/ERC20.sol#L107) function in ERC20 as an example, '_balances' is a mapping where we can retrieve the corresponding value by using the key 'account'.
    
    ```solidity
    function balanceOf(address account) public view virtual returns (uint256) {
        return _balances[account];
    }
    ```
    

### Documentation

```solidity
uint b = balance[address(0x123)];
```

To access the value associated with the key, we use brackets.

***b*** - the value returned by our querying action

***balance*** - the mapping variable 

`address(0x123)` - the key we want to query

### FAQ

# Example/Example

```solidity
pragma solidity ^0.8.4;
contract book {
  //mapping(keyType => valueType) scope mappingName;
  mapping(address => uint) private owned_book;

  function add_book(address owner, uint bookID) public {
    //this will find the book given the owner
    owned_book[owner] = bookID;
  }

  function get_book(address owner) public view returns(uint) {
    //this will find the book given the owner
    return owned_book[owner];
  }
}
```
