# Content/Content

### Concept

A state variable in Solidity is a persistent data **storage location** within a *smart contract* that maintains its value across **multiple** function calls and transactions. 

- Metaphor
    
    A *state variable* in Solidity is like a drawer in a desk, where you can store and retrieve items (data) that remain in the drawer even after you close and reopen it.
    
- Real Use Case
    
    In the ERC20, ***[_totalSupply](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/cec0800c541c809f883a37f2dfb91ec4c90263c5/contracts/token/ERC20/ERC20.sol#L40)*** is a *state variable* that stores the total supply of the token.
    
    ```solidity
    uint256 private _totalSupply;
    ```
    

### Documentation

```solidity
contract ContractName {
  //This is a state variable
  int a; 

  function add(int b) returns(int){
    //b is defined as a parameter, so it's not state variable
    //c is defined in a function, so it's also not a state variable 
    int c = a + b;	
    return c;
  }
}
```

To define a state variable, we need to put it outside of *functions*. 

### FAQ

- When to use State Variables?
    
    If this piece of information should be part of the blockchain, then it should be state variables. *State Variables* are expensive, so make sure that you only set them to be *state variables* when it is worth the money. 
    
- What's the difference between a state variable in Solidity and a global variable in other programming languages?
    
    A *state variable* in Solidity is a data **storage** location on the blockchain that persists across transactions, while a global variable in other programming languages is a data **storage** location within the program's runtime environment that typically does not persist beyond the program's execution.
    

# Example/Example

```solidity
pragma solidity >=0.4.0 <0.9.0;

contract Book {
  int256 bookID;
  bool read;

  // ...
  function a() public returns(int256) {
    // Using State variable, assign value to the container
    bookID = 3;
    // int is a value type, so bookId will also has a value:3
    int256 bookId = bookID;
    return bookId;
  }
}
```
