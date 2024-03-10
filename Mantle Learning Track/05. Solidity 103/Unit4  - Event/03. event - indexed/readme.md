# Content/Content

### Concept

In the previous section, we learned about event broadcasting. In this section, we will continue to learn an event-specific keyword `indexed`.

`Indexed` is a keyword used in *event* *parameters* in Solidity. It allows these *parameters* to be logged and searchable, aiding in event filtering. Solidity permits up to three *indexed parameters* per *event*.

- Metaphor
    
    The *indexed* *parameter* in *events* is like attaching a label to specific envelopes, making it easier to quickly sort and retrieve relevant information when searching through a collection of messages.
    
- Real Use Case
    
    In the ***[Transfer](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/token/ERC20/IERC20.sol#L16)*** function in IERC20 we just mentioned, the ***from*** and ***to*** addresses are declared as indexed. This means that when this *event* is *emitted*, the Ethereum node will store the indexed values of ***from*** and ***to*** in a way that enables faster querying for events based on these *indexed parameters*.
    
    ```solidity
    event Transfer(address indexed from, address indexed to, uint256 value);
    ```
    

### Documentation

In Solidity, the `indexed` keyword can be added after the parameter type in the event declaration, making the parameter searchable.

```solidity
contract IndexedEventContract {
  event LogChange(uint indexed id);

  function changeValue(uint _id) public {
    emit LogChange(_id);
  }
}
```

### FAQ

- Why should we index event parameters?
    
    For example, as a NFT trading platform admin, we may want to index the NFT ID in the transaction event so users could search for all the trading information on a specific NFT. 
    

# Example/Example

```solidity
// SPDX-License-Identifier: GPL-3.0
contract MyContract {
  event MyEvent(address indexed sender, uint value);

  function triggerMyEvent(address _sender, uint _value) public {
    emit MyEvent(_sender,_value);
  }
}
```
