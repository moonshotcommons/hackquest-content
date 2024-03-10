# Content/Content

### Concept

A *function* modifier in Solidity allows you to define reusable pre-conditions or post-conditions that can be applied to multiple *functions* within a *contract*, enhancing code readability and enforcing standardized behavior.

- Metaphor
    
    *Function* *modifier* can be regarded as a guard, checking constraints like whether a specific *address* can access a particular *function* and clean up after the execution. 
    
- Real Use Case
    
    In the ***[Ownable](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/access/Ownable.sol#L48)*** contract provided by OpenZepplin, the ***onlyOwner*** modifier is given, which will check whether the caller is the owner before the contract is executed.
    
    ```solidity
    modifier onlyOwner() {
        _checkOwner();
        _;
    }
    ```
    

### Documentation

To define a *function* *modifier* in Solidity, you use the `modifier` keyword, followed by an identifier, optional parameters, and a body, just like defining a *function*.  

```solidity
contract Example {
  uint public x;

  modifier checkValue(uint _value) {
    require(_value > x, "Value is not greater than x");
    _;
  }
}
```

### FAQ

- When to use *modifer*?
    
    You’re selling some books, as long as people pay more than 10 ETH, you’ll sell them. Now we have a buyBook() function that checks the price paid by the caller is greater than 10 ETH. 
    
    ```solidity
    function buyBook() {
      require(msg.value > 10, "no enough money");
      //buy book
    }
    ```
    
    However, you also sell NFTs. Same rules, For more than 100 ETH, you’ll sell it. Now we have a buyNFT() function that checks the price paid by the caller is more significant than 100 ETH. 
    
    By the way, we also sell hats, cups, and so many different things, and we don’t want to write this required statement every time. 
    
    Now we have a function modifier. 
    

# Example/Example

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.17;

contract Example {
  address public owner;

  modifier onlyOwner() {
    require(msg.sender == owner, "Only the owner can call this function.");
    _;//We will explain this in the next chapter
  }
}
```
