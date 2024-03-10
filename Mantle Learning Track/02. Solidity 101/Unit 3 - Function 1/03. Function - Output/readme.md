# Content/Content

### Concept

Function output refers to the data or values returned by a function after it's executed, providing the result of the function's computations or actions to the caller.

- Metaphor
    
    Function output is akin to the dish prepared from a recipe, representing the outcome that the function has produced based on the provided inputs and its internal processes.
    
- Real Use Case
    
    Similar to the ***[balanceOf**](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/8186c07a83c09046c6fbaa90a035ee47e4d7d785/contracts/token/ERC20/ERC20.sol#L106-L108)* function in ERC20, you input an address to query the balance of that address. The balance needs to be returned to the caller through an output to complete the entire querying process.
    
    ```solidity
    function balanceOf(address account) public view virtual returns (uint256) {
        return _balances[account];
    }
    ```
    

### Documentation

```solidity
//this function returns one signed integer 
function sum(int a, int b) returns(int){
  //return the number
	return 3;
}
```

To define the output of a *function*, we add a `returns` after the parentheses. 

To return the value, we use `return` (no s here in contrast to the function header.) 

### FAQ

- How to return **multiple** values?
    
    You can return **multiple** values from a function using a tuple.
    
    ```solidity
    function getValues() public pure returns (uint256, string memory) {
            uint256 intValue = 42;
            string memory stringValue = "Hello, world!";
            return (intValue, stringValue);
        }
    ```
    

# Example/Example

```solidity
pragma solidity 0.8.4;
contract Function {
  //Here we define a function called add
  //which takes two int, a and b, and outputs another int.
  function add(int a, int b) returns(int) {
    return a + b;
  }
}
```
