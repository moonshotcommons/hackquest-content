# Content/Content

### Concept

In Solidity, delegatecall copies the *function* code from another *contract* to the current *contract* then execute the *function*. 

Since we copied the code into current *contract*, the *function* will be executed in current context thus state variables will be updated by a *function* outside of current *contract*. 

<aside>
💡 This is a very dangerous mode. A lot of attacks have happened in Ethereum due to incorrect use of delegatecall.

</aside>

- Metaphor
    
    Delegate call in Solidity is like borrowing someone else's skills while using your own tools and workspace to get a job done.
    
    Other’s skills (code) will get your job done and wear your tools (update your *state variables*)
    
- Real Use Case
    
    In [***Address library](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/utils/Address.sol#L105)*** , ******delegatecall ******is used execute the function in the current context. 
    
    ```solidity
    function functionDelegateCall(address target, bytes memory data) internal returns (bytes memory) {
    		(bool success, bytes memory returndata) = target.delegatecall(data);
    		return verifyCallResultFromTarget(target, success, returndata);
    }
    ```
    

### Documentation

delegatecall has the same syntax as *low-level call*, we use `address.delegatecall()`

```solidity
//targetAddress is the address of the target contract
//abiEncodedData is the ABI encoding of the call data
(bool success, bytes memory data) = address(targetAddress).delegatecall(abiEncodedData);
```

### FAQ

- When do we need delegatecall?
    
    Once a contract deployed, it cannot be updated. However, what if we want to update the function in the future? In this case, we deploy a contract ***A***, then delegatecall a function in ***B***. If we need to update the function, we only need change the address of ***B*** to ***C*** and ***A*** could use the new function in ***C*** while all the changes are still made in ***A***.
    

# Example/Example

```solidity
pragma solidity ^0.8.0;

contract StorageContract {
  uint public data;

  function setData(uint _data) external {
    data = _data;
  }
}

contract DelegateCallContract {
  uint public storedData;
  address public storageContract;

  //StorageContract的地址
  constructor(address _storageContract) {
    storageContract = _storageContract;
  }

  function dosome(uint _data) external {
    // we use delegatecall to execute setData in current contract
    (bool success, ) = storageContract.delegatecall(abi.encodeWithSignature("setData(uint256)", _data));
    require(success, "DelegateCall failed");

    //after the execution, we notice that data in StorageContract is not assigned
    //but storedData in current contract is assigned
    //this is because the setData is executed in current contract while data correspond
    //to the first parameter in slot0, which is sotredData in this contract
  }
}
```