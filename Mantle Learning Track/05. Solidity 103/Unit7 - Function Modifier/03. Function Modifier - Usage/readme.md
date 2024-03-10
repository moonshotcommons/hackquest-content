# Content/Content

### Concept

*Function modifiers* in Solidity provide a way to amend the behavior of a *function*. They are frequently used to check preconditions (such as access controls or validation of input data) before the execution of a *function*.

They’re applied in the same way as scope or state mutability.

- Metaphor
    
    Using a modifier in a Solidity function is like adding a safety lock to a restricted room, where the lock ensures that only individuals with the right key (modifier conditions) are allowed to enter and perform specific actions (function execution) within the room.
    
- Real Use Case
    
    A ***transferOwnership*** *function* in the ***[OwnableUpgradeable](https://github.com/OpenZeppelin/openzeppelin-contracts-upgradeable/blob/7d7ad99dee371e0ee042e2999aaf43941dea1513/contracts/access/OwnableUpgradeable.sol#L89C1-L94C6)*** contract given by OpenZepplin. It uses the ***onlyOwner*** modifier to ensure that only the current owner (that is, the owner of the contract) can call this *function* to transfer ownership.
    
    ```solidity
    function transferOwnership(address newOwner) public virtual onlyOwner {
            if (newOwner == address(0)) {
                revert OwnableInvalidOwner(address(0));
            }
            _transferOwnership(newOwner);
        }
    ```
    

### Documentation

*Modifiers* are placed just before the function's opening curly braces `{` when defining the function. 

```solidity
modifier aboveMinimumBid {
  require(msg.value >= minimumBid, "Bid is not high enough.");
  _;
}

function bid() public payable aboveMinimumBid {
  // Place the bid
}
```

### FAQ

- Can modifiers be used with constructor?
    
    No, modifiers cannot be applied to constructors. It could only be used with normal functions defined with names, possibility parameters, and returns. 
    

# Example/Example

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.17;
contract TestContract {
  uint public value;

  modifier greaterThanValue(uint _value) {
    require(_value > value, "Input should be greater than value.");
    _;
  }

  function setValue(uint _value) public greaterThanValue(_value) {
    value = _value;
  }
}
```
