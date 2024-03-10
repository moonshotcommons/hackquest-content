# Content/Content

### Concept

The fallback function in Solidity is a special *function* in a *contract* that is executed under three scenarios:

1. the caller tries to call a *function* that doesn’t exist
2. Ether is sent but the receiver function doesn’t exist
3. Ether is sent, the receiver function exists, but msg.data is not empty

```solidity
Receiving ETH 
|
Is msg.data empty? 
/                  \
Yes                no
/                     \
receive() exist?       fallback()
/              \
Yes            No
/                \
receive()      fallback()
```

- Metaphor
    
    The *function call* is like delivering a package. If the *address* is clear, the package is delivered. If the *address* is ambiguous or doesn’t exist, there is a default place for the package to go to. The fallback function is like this default place.  
    
- Real Use Case
    
    In the [***Proxy***](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/proxy/Proxy.sol#L66C1-L68C6) *contract*, we use the fallback **function to delegate function calls. All the *function calls* will be executed in another *contract* through fallback because our ***Proxy*** contract **only contains *internal functions* (except the *fallback function*).
    
    ```solidity
    /**
     * @dev Fallback function that delegates calls to the address returned by `_implementation()`. Will run if no other
     * function in the contract matches the call data.
     */
    fallback() external payable virtual {
        _fallback();
    }
    ```
    

### Documentation

```solidity
fallback() external { }
```

To define a fallback **function, you need the keyword `fallback`. Fallback *functions* don’t take any *parameters* and need to be defined as `external`. 

### FAQ

- Will solidity create an empty fallback function for you if you don’t define one? like, *constructor*?
    
    No, unlike a *constructor*, if you don’t define a fallback function and you try to use it, there will be an error. This is to prevent unexpected behavior like sending Ether to a contract that is not able to be retrieved. 
    
- Fallback vs. Receive
    
    receive is an updated feature in Solidity after *0.6.x* . You should use receive to receive ether transfer and use fallback to handle situations where Ether is not involved. 
    
    <aside>
    💡 If you call an undefined function using *low level call*, and there’s no receive, and the fallback is not *payable*, the contract will reject the ETH and your transaction will fail
    
    </aside>
    

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
  function callReceive(address _contract) external {
    // call a function that doesn't exist in ContractA
    bytes memory encodedData = abi.encodeWithSignature("nonExistentFunction()");
    //since we're sending ETH and we have data, fallback will be executed
    (bool suc,) = _contract.call{value: 1}(encodedData);
    require(suc, "call fail");
  }
}
```