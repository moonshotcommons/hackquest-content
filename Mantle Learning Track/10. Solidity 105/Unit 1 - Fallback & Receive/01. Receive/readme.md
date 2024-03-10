# Content/Content

### Concept ****

The receive function is a particular *function* executed when someone sends Ether to the *contract* without providing any additional data. 

It's typically used to accept Ether.

- Metaphor
    
    The receive function in Solidity is like a mailbox for a *smart contract*, where it can accept and process incoming Ether transactions just like a mailbox collects and holds incoming letters.
    
- Real Use Case
    
    In the ***[Governor](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/governance/Governor.sol#L82)*** contract by OpenZeppelin, we have a receive function to receive the ETH that will be handled by the governor.  
    
    ```solidity
    /**
    * @dev Function to receive ETH that will be handled by the governor (disabled if executor is a third party contract)
    */
    receive() external payable virtual {
      if (_executor() != address(this)) {
          revert GovernorDisabledDeposit();
      }
    }
    ```
    

### Documentation

A receive function has no name, takes no parameters, and returns nothing. It must be marked as `external` and `payable`.

```solidity
receive() external payable { }
```

# Example/Example

```solidity
pragma solidity ^0.8.0;

contract ContractA {
  bool public flag;
  //fallback function
  fallback() external payable{
    flag = false;
  }
  //receive function
  receive() external payable {
    flag = true;
  }
}

contract ContractB {
  function callReceive(address _contract) external payable {
    //since we're sending ETH with no parameter and we have receive, receive will be executed
    (bool suc,) = _contract.call{value: 1}("");
    require(suc, "call fail");
  }
}
```