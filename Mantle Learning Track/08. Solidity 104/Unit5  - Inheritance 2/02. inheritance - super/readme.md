# Content/Content

### Concept

In this section, we'll explore using `super` to call *parent contract functions* and *variables*.

In Solidity, `super` is a keyword used in a child contract to access and call *functions* or *variables* from the *parent contract*. It ensures that the original behavior defined in the parent contract is executed while allowing for extension or modification in the *child contract*.

- Metaphor
    
    For example, you work as a cashier at a small store. The store introduces a new service: membership discounts for customers. As an employee, you must apply the membership discount and then handle cash transactions as before.
    
    The traditional payment amount is like the payment *function* in the *base contract*, now we override the payment *function* with a discount. `Super` is still calling the traditional payment *function* in the *base contract* although the system has been updated. 
    
- Real Use Case
    
    Still the same example, this *function* uses the syntax **`super._beforeTokenTransfer(from, to, amount);` This will call ***_beforeTokenTransfer*** in [ERC20](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/fd81a96f01cc42ef1c9a5399364968d0e07e9e90/contracts/token/ERC20/ERC20.sol#L348).
    
    ```solidity
    function _beforeTokenTransfer(address from, address to, uint256 amount)
        internal
        whenNotPaused
        override
    {
        super._beforeTokenTransfer(from, to, amount);
    }
    ```
    

### Documentation

Using `super.functionName` allows you to call the same *function* in the *parent contract*.

```solidity
//Here, we call the init function in the parent contract.
super.init()
```

<aside>
💡 In multiple inheritance, `super` refers to the *contract* written at the end. When a *function* is called using `super`, it will search for the *function* in the order of *contract* *inheritance* from **right to left**.

</aside>

### FAQ

- What does super do in Solidity contracts?
    
    The `super` keyword in Solidity allows a derived *contract* to call a *function* from its immediate *parent contract*. This enables you to extend and build upon the *parent contract's* functionality without rewriting it.
    
- When should I use super in Solidity?
    
    Use `super` when you want to override a *function* in a *derived contract* while still keeping the logic from the *parent contract* intact. It allows you to add additional functionality in the *derived contract* without disrupting the original behavior.
    

# Example/Example

```solidity
pragma solidity ^0.8.0;

contract Parent {
  function foo() public virtual returns (string memory) {
    return "Parent";
  }
}

contract Child is Parent {

  function foo() public override returns (string memory) {
    return super.foo();
  }
}
```
