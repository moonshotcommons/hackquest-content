# Content/Content

### Concept

A mapping in Solidity is a **key-value data** structure that allows efficient storage and retrieval of data, where each key corresponds to a **unique value.**

- Metaphor
    
    Imagine you’re a bank. You’ll need to keep track of the balance of all accounts (represented by address). 
    
    Very frequently, you want to look up the balance given the account, but normally, there’s no scenario that given the balance you want to look up the account. This is a one-way association.  
    
- Real Use Case
    
    In an ERC20 contract, the ***[balances](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/8186c07a83c09046c6fbaa90a035ee47e4d7d785/contracts/token/ERC20/ERC20.sol#L39)*** mapping is used to store the token balances of various addresses. The keys (addresses) are associated with their respective token balances (uint).
    
    It provides one way association between two types —— address and uint here.
    
    ```solidity
    mapping(address => uint) balances;
    ```
    
    Here, the address is called the `key` type and uint is the `value` type. 
    

### Documentation

```solidity
mapping(uint => uint) IDToID;
```

To define a mapping, we use keyword `mapping`, followed by the two types that we want to build a one-way association between. Finally the name at the end. 

### FAQ

- Could we have a mapping as the key or value type of **another mapping**?
    
    Yes, you could. In Solidity, you can use a mapping as either the key or value type of another mapping. This is often referred to as a "nested mapping" or "mapping of mappings." It allows you to create more complex data structures that provide efficient ways to organize and access data.
    
    ```solidity
    mapping(address => mapping(uint256 => uint256)) public nestedMapping;
    ```
    
- What if I want to use a key to look up values, but also use values to look up keys?
    
    You should have two mappings in this case.
    

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
