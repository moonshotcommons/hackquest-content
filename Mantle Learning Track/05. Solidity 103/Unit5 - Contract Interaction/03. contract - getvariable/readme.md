# Content/Content

### Concept

In Solidity, a *contract variable* lets you interact with another *contract*, which includes not only calling its *functions* but also accessing its *state variables*. 

<aside>
💡 Only `state variables` declared as `public` are accessible from other `contracts`.

</aside>

- Metaphor
    
    Using a contract variable to access a state variable of another contract in Solidity is like having a remote control to view and adjust the settings of a distant device.
    
- Real Use Case
    
    Still using the previous example, if we want to get the value of the ***_minDelay*** variable of the ***[TimelockController](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/governance/TimelockController.sol#L24)*** contract, we can use the following method:
    
    ```solidity
    _timelock._minDelay();
    ```
    

### Documentation

To access a *state variable* of a contract through a *contract variable*, you use the name of the *contract* variable, followed by a dot ***`.`***, and then the *state variable* name followed by **`()`.

```solidity
contract NFTContract {
  uint public totalSupply;
}

contract MarketplaceContract {
  NFTContract public nft;

  function getTotalSupply() public view returns (uint) {
    return nft.totalSupply();
  }
}
```

### FAQ

- Why do we need to have `()` when calling another contract’s state variables?
    
    This is because when you have a public state variable, Solidity actually will create a getter function for you, and when you access the variable from another contract, you’re calling the getter function to retrieve the value. 
    
    [https://docs.soliditylang.org/en/latest/contracts.html#visibility-and-getters](https://docs.soliditylang.org/en/latest/contracts.html#visibility-and-getters) 
    
- Why do we need to access state variables through contract variables?
    
    Accessing *state variables* through *contract* variables is a fundamental part of building complex decentralized applications. It allows *contracts* to read the state of other contracts, informing their own logic and decision-making processes.
    

# Example/Example

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.17;

contract Token {
  uint public totalSupply;

  constructor(uint _totalSupply) {
    totalSupply = _totalSupply;
  }
}

contract TokenReader {
  Token public token;

  constructor(Token _token) {
    token = _token;
  }

  function readTotalSupply() public view returns (uint) {
    return token.totalSupply();
  }
}
```
