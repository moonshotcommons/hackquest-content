# Content/Content

### Concept

Function input refers to the values or data provided to a function when it is called, which the function can use to perform computations, make decisions, or update the contract's state.

- Metaphor
    
    Function input in Solidity is like ingredients you provide to a recipe, enabling the function to create a specific outcome based on what you've supplied.
    
- Real Use Case
    
    For example, the ***[balanceOf](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/8186c07a83c09046c6fbaa90a035ee47e4d7d785/contracts/token/ERC20/ERC20.sol#L106C1-L106C1)*** function takes an ***_account*** address as input and returns the token balance associated with that address.
    
    ```solidity
    function balanceOf(address account) public view virtual returns (uint256) {
        return _balances[account];
    }
    ```
    

### Documentation

```solidity
//Here we have two inputs, a, and b, both are signed integers int
function sum(int a, int b) {
  //function body 
}
```

To define the input of a function, we put them in parentheses after the name of the *function*.

If we want multiple *parameters*, then we use`,` to separate them. 

### FAQ

# Example/Example

```solidity
pragma solidity ^0.8.4;
contract Function {
  //Here we define a function called add, which takes two int,
  //a and b, and outputs another int.
  function add(int a, int b, bool c, address d) public returns(int){
    return a + b;
  }
}
```
