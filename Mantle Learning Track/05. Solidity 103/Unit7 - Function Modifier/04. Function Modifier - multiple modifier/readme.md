# Content/Content

### Concept

A single *function* can have multiple modifiers. The modifiers are executed in the order they appear.

- Metaphor
    
    Multiple modifiers in a Solidity function are like layers of security clearance at different checkpoints, where each modifier represents a specific level of authorization that must be granted before gaining access to the guarded area (function execution).
    
- Real Use Case
    
    In this contract, the ***changeOwner*** *function* has two *modifiers*: ***onlyOwner*** and ***onlyAfterOneHour***. The ***onlyOwner*** *modifier* restricts the function to be callable only by the owner. The ***onlyAfterOneHour*** *modifier* restricts the function to be callable only one hour after *contract* deployment. The *modifiers* are executed in the order they are listed.
    
    ```solidity
    contract MultiModifierContract {
      address public owner;
      uint public creationTime;
    
      constructor() {
        owner = msg.sender;
        creationTime = block.timestamp;
      }
    
      modifier onlyOwner {
        require(msg.sender == owner, "Only owner can execute.");
        _;
      }
    
      modifier onlyAfterOneHour {
        require(block.timestamp >= creationTime + 1 hours, "Function can only be called after one hour.");
        _;
      }
    
      function changeOwner(address _newOwner) public onlyOwner onlyAfterOneHour {
        owner = _newOwner;
      }
    }
    ```
    

### Documentation

When a *function* has multiple *modifiers*, they are written separated by a space and are applied in the order in which they appear.

```solidity
function bid() public payable aboveMinimumBid beforeAuctionEnd {
    // Place the bid
}
```

### FAQ

- How many modifiers could a function have?
    
    Theoretically, you could have as many as you want, but there’re practical limit on this, for example: gas limit or stack depth.  
    

# Example/Example

```solidity
pragma solidity ^0.8.0;

contract MyContract {
  address public owner;

  constructor() {
    owner = msg.sender;
  }

  modifier onlyOwner() {
    require(msg.sender == owner, "Only owner can call this function.");
    _;
  }

  modifier notNull(address newOwner) {
    require(newOwner != address(0), "New owner's address must not be zero.");
    _;
  }

  function changeOwner(address newOwner) public onlyOwner notNull(newOwner) {
    owner = newOwner;
  }
}
```
