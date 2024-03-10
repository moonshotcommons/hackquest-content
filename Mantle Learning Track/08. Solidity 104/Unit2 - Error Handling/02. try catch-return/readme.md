# Content/Content

### Concept

In Solidity, the `try-catch` mechanism offers a structure to not only handle errors in external function calls but also to deal with the *returned* values of these calls. This is aptly called the *try-catch-return* pattern.

When interacting with *external functions* (calls to other *contracts*), you often expect a specific return value if the call is successful. However, the call might also fail for various reasons.

- Metaphor
    
    Imagine you're at a vending machine, ready to buy a can of soda.
    
    Try: You insert a dollar into the machine and press the button for your desired soda.
    
    Catch:
    
    Success Scenario: The vending machine processes the transaction, recognizes the money, and tries to dispense the soda. If it has the soda in stock, you get your drink.
    
    Error Scenario: If the specific slot is empty (soda out of stock), the vending machine doesn't just keep your money. It triggers an error mechanism.
    
    Return:
    
    Success Return: You get your soda.
    
    Error Return: The machine returns your dollar and possibly displays an "Out of Stock" message.
    

### Documentation

`try` a function with a return value.

```solidity
// Capture return value from 'try'. If `f()` succeeds, assign its return to 'val'.
uint val;
try externalContract.f() returns(uint _val) {
    val = _val;
} catch {

}
```

### FAQ

- How does the return mechanism work with try-catch?
    
    In the `try` part of the mechanism, you can specify return values using the `returns` keyword. If the external call is successful and *returns* a value, the *returned* value is processed inside the `try` block. If the call fails, the control moves to the `catch` block, and the value *returned* from the failed call is disregarded. Instead, the `catch` block can return its own value or message to provide feedback about the error.
    
- Does the try-catch-return pattern always require a return statement in the catch block?
    
    Not always. The necessity of a `return` statement in the `catch` block depends on your function's signature. If your *function* declares that it will *return* values, then you should ensure that all code paths (including the `catch` blocks) provide a *return* value. 
    
- How can I handle multiple return types or values in try-catch-return?
    
    The return values in the `try` block need to match the *return* values of the *function* being called. If the *function* has multiple *return* values, you can specify them using a `tuple`. If an error occurs, the `catch` block should *return* values that match the same type and order as the original function signature.
    

# Example/Example

```solidity
pragma solidity ^0.8.0;

contract PaymentExample {

  bool public val = false;
  function sendEther(address contractB) public {
    try B(contractB).dosome() returns(bool ret) {
      //send success
      val = ret;
    } catch {
      //send failed
    }
  }
}

contract B {
  function dosome() public pure returns(bool){
    return true;
  }
}
```
