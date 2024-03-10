# Content/Content

### Concept

In the previous section, we learned about the global variable *block.number*, which is used to obtain the current block height.

In this section, we will learn another block's *global variable* `block.timestamp`, representing the seconds elapsed since 00:00:00 UTC, 1 January 1970, of the currently mined block. 

<aside>
💡 Block timestamps can be manipulated (within a certain limit) by miners.

</aside>

- Metaphor
    
    The *block.timestamp* is akin to the timestamp on a photograph, representing the exact moment a block is added to the blockchain and capturing the time at which a specific event or transaction occurred within the network's timeline.
    
- Real Use Case
    
    In OpenZepplin's [***ERC20Permit***](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/token/ERC20/extensions/ERC20Permit.sol#L44) contract, an expiration time is set. When executing the ***permit***, it will be judged whether the current time has expired. If it has expired, it will `revert` and roll back.
    
    ```solidity
    function permit(
        ...
    ) public virtual {
        ...
        if (block.timestamp > deadline) {
            revert ERC2612ExpiredSignature(deadline);
        }
    }
    ```
    

### Documentation

`block.timestamp` is a *global variable* in Solidity that denotes the current block's timestamp.

```solidity
function processBlock() public {
  uint time = block.timestamp;
  // currentTimestamp now holds the timestamp of the current block
}
```

### FAQ

- What is the difference between timestamp and block.number?
    
    One is in seconds, the other is in block numbers, and their units of measuring time are inconsistent.
    
    It should be noted that on different chains, the time measured by *block.number* is different.
    
    But the time measured by *block.timestamp* is consistent. 
    

# Example/Example

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.17;

contract BlockTimestampExample {
  function showCurrentBlockTimestamp() public view returns (uint) {
    return block.timestamp;
  }
}
```
