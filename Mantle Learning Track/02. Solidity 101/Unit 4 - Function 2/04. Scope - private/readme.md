# Content/Content

### Concept

*Variables* defined as private can only be accessed within the contract.

- Metaphor
    
    Come back to our household example, private functions and variables are like inside jokes that can only be accessed by people within the household. 
    
- Real Use Case
    
    ```solidity
    uint256 private _totalSupply;
    ```
    
    In the ERC20 contract, the ***[_totalSupply](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/8186c07a83c09046c6fbaa90a035ee47e4d7d785/contracts/token/ERC20/ERC20.sol#L43)*** state variable is marked as `private`, preventing **direct** access from external contracts. It can only be accessed from within the contract itself.
    

### Documentation

To define a *private variable* or *function*, we use the keyword `private`.

```solidity
uint private a;
function aa() private {
  //funciton body 
}
```

### FAQ

- What are the other scopes, other than public and private?
    
    The scope for a function or variable could also be `internal` or `external`. Sometimes we want this function to be called by other functions in the same contract, in this case we will set it to be external. If we only expect the function to be called from current contract and contracts inheriting this one, we set it to be internal. 
    

# Example/Example

```solidity
pragma solidity ^0.8.4;
//If we put the code in Remix and deploy it
//we cannot see b and bbb because they are private. 
contract A {
  uint private b;
  
  function bbb() private {
    b++;
  }
}
```
