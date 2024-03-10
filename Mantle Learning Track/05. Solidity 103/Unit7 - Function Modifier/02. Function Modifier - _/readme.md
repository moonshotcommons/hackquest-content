# Content/Content

### Concept

The _ symbol in a *function modifier* plays a crucial role - it's a placeholder that represents the *function* that the *modifier* is being applied to. 

When the *function* with the *modifier* is called, the code before _ in the modifier runs first. After that, if all conditions in the *modifier* are satisfied, the code in the *function* runs.

- Metaphor
    
    The underscore (`_`) in a *function modifier* is like a placeholder slot in a recipe that gets filled with the actual cooking instructions (*function* logic) after the special preparation steps (*modifier conditions*) are completed, ensuring the recipe is followed correctly.
    
- Real Use Case
    
    Still the same ***[Ownable](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/access/Ownable.sol#L48)*** contract, in the ***onlyOwner*** modifier, `_;` indicates the code to run the function body, and `_checkOwner();` before `_;` proves that the check is run before the function is executed.
    
    ```solidity
    modifier onlyOwner() {
        _checkOwner();
        _;
    }
    ```
    

### Documentation

The **`_`** in a *function modifier* is a placeholder that represents the *function* that the *modifier* is being applied to.

```solidity
modifier checkValue(uint _value) {
  require(_value > x, "Value is not greater than x");
  _;
}
```

### FAQ

- Could we also have code after the `_`?
    
    Yes. You could have code both before and after `_`. 
    
    ```solidity
    modifier checkValue(uint _value) {
      require(_value > x, "Value is not greater than x");
      _;
    	emit FunctionCalled();
    }
    ```
    
- Does the order of modifiers in a Solidity function affect its execution?
    
    Yes, the order of modifiers in a Solidity function is crucial and impacts the function's execution. Modifiers are applied in the order they are listed in the function declaration. Consider the following simple example:
    
    ```solidity
    modifier firstModifier() {
        // First modifier logic
        _;
    }
    
    modifier secondModifier() {
        // Second modifier logic
        _;
    }
    
    function myFunction() firstModifier secondModifier {
        // Function code
    }
    ```
    
    In this code, when `myFunction()` is called, `firstModifier` is executed first, followed by `secondModifier`, and finally, the code within `myFunction()` is run. If `firstModifier` includes a condition that fails, the execution will revert before `secondModifier` or the function code is reached. Thus, the arrangement of modifiers affects the logic flow and behavior of the function.
    

# Example/Example

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.17;

contract Example {
  address public owner;

  modifier onlyOwner() {
    require(msg.sender == owner, "Only the owner can call this function.");
    _;
  }
}
```
