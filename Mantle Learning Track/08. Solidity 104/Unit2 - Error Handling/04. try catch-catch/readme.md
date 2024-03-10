# Content/Content

### Concept

In a nested `try-catch` setup, a `try` block is followed by one or more `catch` blocks. Inside a `catch` block, you can place another `try-catch` block to perform additional operations that might also fail.

- Metaphor
    
    Imagine you're a juggler juggling balls in the air. If you drop a ball (analogous to the main `try` block encountering an error), you try to catch it with a net (the first `catch` block). If the net has a hole and the ball slips through (the first `catch` block also encounters an error), you have a trampoline below (the nested `try-catch` within the first `catch`) as a second line of defense to bounce the ball back to you.
    
- Real Use Case
    
    Suppose your [ERC-20](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/ERC20.sol) *contract* needs to interact with a **Decentralized Exchange (DEX)** *contract*. In such a case, you might use `try-catch` to ensure that the success or failure of a trade can be properly handled.
    

### Documentation

`catch{...}`: If you are not interested in the error data, you can just use `catch{...}` (even as the only `catch` clause) instead of the previous clause.

```solidity
try transfer(addr,amount) {

} catch Error(string memory err) {
  // handle errors caused by require or revert ****statement
} catch {
  //other conditions
}

function transfer(address addr, uint amount){
  //catch above will be executed
  assert(addr != address(0));
}
```

### FAQ

- Can I nest try-catch blocks?
    
    Yes, `try-catch` blocks can be nested, meaning you can have a `try-catch` block within another `try-catch` block. This can be useful for handling exceptions at different levels of granularity.
    
- Is it possible to catch custom exceptions?
    
    Yes, you can define and throw custom exceptions in most languages. You can then catch **these exceptions in the same way as built-in exception types.
    

# Example/Example

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.0;

error SpecificNumerator(string msg);

contract ErrorHandlingExample {
  uint public result;

  function divide(uint numerator, uint denominator) external {
    try this.safeDivide(numerator, denominator) returns (uint quotient) {
      result = quotient;
    } catch Error(string memory /*reason*/) {
      //  handle revert() and require()
      result = 11;
    } catch (bytes memory /*lowLevelData*/) {
      // handle custome error and others
      result = 22;
    }
  }

  function safeDivide(uint numerator, uint denominator) external pure returns (uint) {
    require(denominator != 0, "Division by zero");
    if(numerator == 99 ) {
      revert("the numerator is 99");
    }

     if(numerator == 88 ) {
      revert SpecificNumerator("the numerator is 88");
    }

    assert(numerator >= denominator);

    return numerator / denominator;
  }
}
```
