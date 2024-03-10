# Content/Content

### Concept

In Solidity, a contract variable lets you call the *functions* of the *contract*. This is how *smart contracts* on the Ethereum blockchain can interact with each other.

- Metaphor
    
    A function call in Solidity is like instructing a robot to perform a specific task by providing it with precise directions and any necessary materials.
    
- Real Use Case
    
    Also in the [***GovernorTimelockControl***](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/governance/extensions/GovernorTimelockControl.sol#L25) contract, use the ***_timelock*** contract variable just defined to call the ***getMinDelay*** *function* of the ***[TimelockController](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/governance/TimelockController.sol#L24)*** contract.
    
    ```solidity
    function _queueOperations(
        ....
    ) internal virtual override returns (uint48) {
        uint256 delay = _timelock.getMinDelay();
        ...
    }
    ```
    

### Documentation

To call a *function* of a *contract* through a *contract variable*, you use the name of the *contract variable*, followed by a dot `.` , then the *function* name and arguments.

```solidity
contract DigitalAssetContract {
  function transferOwnership(address newOwner) public {
    // ...
  }
}

contract MarketplaceContract {
  DigitalAssetContract public digitalAsset;

  function executeTrade(address newOwner) public {
    digitalAsset.transferOwnership(newOwner);
  }
}
```

### FAQ

- Could we call a function without defining a contract variable?
    
    Yes. You could do low-level calls which we will explain in Solidity 105 and you could call a function through contract address and function selector (kind of like function identifier). 
    
- Why do we need to call functions through contract variables?
    
    *Function* calls through *contract* variables are essential for building complex decentralized applications. They allow *contracts* to modify the state of other contracts or trigger logic defined in them.
    

# Example/Example

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.17;

contract Token {
  mapping(address => uint) public balances;
  bool public transferCalled = false;

  function transfer(address to, uint amount) public {
    // Implement transfer logic...
    transferCalled = true;
  }
}

contract Wallet {
  Token public token;

  constructor(Token _token) {
    token = _token;
   }

  function transferTokens(address to, uint amount) public {
    token.transfer(to, amount);
  }
}
```
