# Content/Content

### Concept

In this unit, we will learn about event. 

*Events* in Solidity allow you to  log and monitor specific changes, such as contract *function* calls or transactions.  This information can be used for client-side applications (dApps) to track transaction execution. 

- Metaphor
    
    Events are like a radio broadcast. When something important happens, it sends out a message with specific details that others can tune into and listen for.
    
- Real Use Case
    
    In the IERC20 contract, this line of code defines an Ethereum event named ***[Transfer](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/token/ERC20/IERC20.sol#L16C77-L16C77)*** that is emitted when a transfer of a specific token value occurs between two addresses (`from` and `to`). 
    
    The *event* provides information about the sender, receiver, and the amount of tokens transferred, making it easier to track and monitor token movements on the blockchain. 
    
    ```solidity
    event Transfer(address indexed from, address indexed to, uint256 value);
    ```
    

### Documentation

*Events* are declared in Solidity with the `event` keyword. 

```solidity
event LogChange(uint value);
```

### FAQ

- When should we use events?
    
    In an NFT trading platform, an *event* could log transaction information, for example A buys B’s NFT number 21, an event might be emitted, notifying all parties involved, then the trading platform’s website could update the owner on the website after received this event.
    

# Example/Example

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.17;

contract EventExample {
  event LogValue(uint value);
}
```
