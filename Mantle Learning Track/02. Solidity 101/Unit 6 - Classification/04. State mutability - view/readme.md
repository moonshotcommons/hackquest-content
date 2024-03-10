# Content/Content

### Concept

A view function reads *state variables* but doesn’t write to them. 

- Metaphor
    
    Think of it as your mom, who could answer your questions about cake making but is not actually doing anything. 
    
    If your *function* tells you something but doesn’t make any changes to the blockchain, then it is a *view function*.
    
- Real Use Case
    
    ```solidity
    function totalSupply() public view virtual returns (uint256) {
        return _totalSupply;
    }
    ```
    
    The ***[totalSupply](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/token/ERC20/ERC20.sol#L99)*** function in the ERC20 contract returns the total supply of the token. 
    
    It is marked as `view` because it **only reads data** from the contract's state and doesn't modify it.
    

### Documentation

```solidity
function totalSupply() public view virtual returns (uint256) {
    return _totalSupply;
}
```

In the ERC20 contract, the ***[totalSupply](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/token/ERC20/ERC20.sol#L99)*** function is used to return the total supply of the token. Because it accesses the state variable ***_totalSupply***, it cannot be declared as 'pure' and should instead be declared as 'view'.

### FAQ

- What is the difference between pure function and view function?
    
    View functions don’t modify (write) the *variables* outside the *function*, but may use (read) the information outside, while *pure functions* don’t even read the data outside the *function*. 
    
    Think of *view functions* as using a one-way cable, that could only charge from one end to another. All the other *functions* need a two-way cable.
    
    <aside>
    💡 If a *function* is *pure*, then it’s also a *view function*.
    
    </aside>
    

# Example/Example

```solidity
pragma solidity ^0.8.0;
contract Example {
  int c = 10;
  //This is a pure function
  function add(int a, int b) public pure returns(int) {
    return a + b;
  }
  //This is a view function, but it's not a pure function 
  function addView(int a) public view returns(int) {
    //c is outside the function, and this is using information outside this function
    //so not pure, but we're not modifying the information, so it's view 
    return a + c;
  }
  //This is neither pure nor view 
  function addNotPure(int a, int b) public returns(int) {
    //c is outside the function and we're modyfing the information  
    c =a + b;
    return c;
  }
}
```
