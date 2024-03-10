# Content/Content

### Concept

In the previous section, we learned the definition of the event, so next, let us learn how to broadcast an event.

A defined event remains dormant until it's broadcasted or *emitted* with all required information. Emitting an *event* triggers it, logging details on the blockchain for transaction tracking in client-side applications.

```solidity
emit MyEvent(_level, _value);
```

- Metaphor
    
    Using emit in Solidity is like lighting a beacon in the dark – it signals an *event* within a *smart contract*, making it visible and trackable to external observers, similar to how a lit beacon is easily noticeable and provides information to distant onlookers.
    
- Real Use Case
    
    The ***[_update](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/token/ERC20/ERC20.sol#L244C20-L244C20)*** function in the ERC20 *contract* may emit the ***Transfer*** *event* to transfer a ***value*** amount of tokens from ***from*** to ***to***.
    
    ```solidity
    function _update(address from, address to, uint256 value) internal virtual {
        ...
        emit Transfer(from, to, value);
    }
    ```
    

### Documentation

In Solidity, *events* are emitted using the `emit` keyword, followed by the *event* name and the specific arguments corresponding to the defined *event parameters*.

```solidity
contract EmitEventContract {
  event LogChange(uint value);

  function changeValue(uint _value) public {
    emit LogChange(_value);
  }
}
```

### FAQ

- When should we emit events?
    
    In the NFT example earlier, after we defined an *event* about the transaction, we need to emit it every time a transaction happens. 
    
- Where could we see the log of events emitted in smart contracts?
    
    When an event is submitted, the event parameters are stored in the transaction log. These logs are associated with the contract’s address and recorded into the blockchain. You can use tools to assist in querying, such as etherscan, etc.
    
- What is the internal mechanism of emit in Solidity?
    
    In Solidity, emit generates a log entry in the transaction log on the blockchain. These logs are part of the transaction receipt and provide a way for external observers to track contract activities. They are stored separately from the contract's state and do not change it, but offer a gas-efficient method for recording important events.
    

# Example/Example

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.17;

contract EmitEventExample {
  event LogValue(uint value);

  function triggerLogValue(uint _value) public {
    emit LogValue(_value);
  }
}
```
