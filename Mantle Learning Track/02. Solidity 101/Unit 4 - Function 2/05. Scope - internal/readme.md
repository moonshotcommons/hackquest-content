# Content/Content

In Solidity, the keywords for specifying the visibility or scope of *functions* or *variables* are also `internal` and `external`. Sometimes we will limit certain *variables* or *functions* to be used only in internal contracts.

`Internal` functions and variables are accessible within the contract they are defined in, as well as in any contracts that inherit from it (inheritance will be covered later).”

- Metaphor
    
    `Internal` is like your bedroom, only you and your family can enter and no one from outside can enter. Your bedroom is private and cannot be accessed by others.
    
    <aside>
    💡 Inherited contracts can also call *functions* marked `internal`.
    
    </aside>
    
- Real Use Case
    
    There are `internal` functions such as ***[_transfer](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/8186c07a83c09046c6fbaa90a035ee47e4d7d785/contracts/token/ERC20/ERC20.sol#L228)*** in ERC20, which are only used within the contract to ensure the security of token transfers.
    
    ```solidity
    function _transfer(address from, address to, uint256 value) internal {
            if (from == address(0)) {
                revert ERC20InvalidSender(address(0));
            }
            if (to == address(0)) {
                revert ERC20InvalidReceiver(address(0));
            }
            _update(from, to, value);
    }
    ```
    

### Documentation

In Solidity, the `internal` keyword controls the visibility of both functions and state variables:

- Internal Functions: To define a *function* that is only used inside the *contract*, we use the keyword `internal` and place it after the *function parameters*. When using, you can directly use the `funcName()` to call the *function*.
    
    ```solidity
       function aa() internal{}
    
       aa();
    ```
    
- Internal Variables: Similar to `internal` functions, `internal` state variables are accessible within the contract where they are declared and in any derived contracts. They cannot be accessed externally, ensuring controlled interaction with the contract's state.
    
    ```solidity
    uint256 internal internalVar;
    ```
    

### **FAQ**

- Why do we need to distinguish between external and internal?
    
    To control access and improve security. Some *functions* need to be used by other *contracts*, while some *functions* should only be used within the current contract. By defining different visibility, we can ensure that the *contract’s* data and functionality are only accessed in the appropriate context, thereby enhancing the security and maintainability of *smart contracts*.
    

# Example/Example

```solidity
pragma solidity ^0.8.4;
contract A {

    uint public result;

    function aa(uint a) internal {
        result = a + 1;
    }

    function b(uint b) public {
         aa(b);
    }
}
```
