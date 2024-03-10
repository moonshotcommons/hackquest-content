# Content/Content

### Concept

A low-level call in Solidity refers to the direct interaction with *external contracts* at the *contract bytecode* level. 

It involves invoking *functions* or sending transactions to other *contracts* using the `call` *function*, allowing for more granular control over gas management, return data handling, and error checking compared to higher-level Solidity function calls.

- Metaphor
    
    Think of making a normal *function call* of another *contract* as calling a taxi and tell the driver your destination. Making a low-level call is like direct the drive to turn left as this crossing, and straight for another 2 miles, the turn right and make a stop. 
    
    In Solidity, we could either define the *contract* and make the *function call* through *function* name, or we use `contractAddress.call(data);` directly to make the *function call*. 
    
- Real Use Case
    
    In the ***[ReentrancyMock](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/mocks/ReentrancyMock.sol#L29)*** contract, we see that *low-level call* is used to call itself.
    
    This is a mock *contract*, and each time the *low level call* happens ***n*** is decreased by *1*. 
    
    ```solidity
    function countThisRecursive(uint256 n) public nonReentrant {
        if (n > 0) {
            _count();
            (bool success, ) = address(this).call(abi.encodeCall(this.countThisRecursive, (n - 1)));
            require(success, "ReentrancyMock: failed call");
        }
    }
    ```
    

### Documentation

**Low-level call** is made with `address.call()` that takes three *parameters*:

- targetAddress is the *address* of the target contract
- value: specifies the amount of Ether we’d like to send along the *function call*
- abiEncodedData: is the ABI encode of the call data, encoded with `abi.encodeWithSignature` or `abi.encodeWithSelector`

It returns two values:

- success: a *bool* indicating whether the *low-level call* is success or not
- data: the return value of the call

```solidity
(bool success, bytes memory data) = address(targetAddress).call{value: amount}(abiEncodedData);
```

### FAQ

- When do we want to use low-level call?
    
    When we don’t want to define the entire contract in our file just to make one function call. 
    
    I would like to buy an NFT from the NFT contract, but I don’t want to define the IERC721 and the NFT contract just to buy an NFT. Here I could just do low-level call.
    
- What is abiEncodedData?
    
    This is the data needed for low-level call, it includes two parts: function signature and parameters.
    
    There’re two way to get the function signature, either with `abi.encodeWithSignature` or `abi.encodeWithSelector`.
    
    ```solidity
    abi.encodeWithSignature("myFunction(uint256,string)", 123, "Hello");
    abi.encodeWithSelector(bytes4(keccak256("myFunction(uint256,string)")),123, "Hello");
    ```
    

# Example/Example

```solidity
pragma solidity ^0.8.0;
contract TargetContract {
  uint256 public value;

  function setValue(uint256 newValue) external {
    value = newValue;
  }
}

contract CallerContract {
  function callTargetContract(address targetAddress, uint256 newValue) external {
    bytes memory payload = abi.encodeWithSignature("setValue(uint256)", newValue);
    (bool success, ) = targetAddress.call(payload);
    require(success, "Call to target contract failed");
  }
}
```