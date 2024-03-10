# Content/Content

### Concept

msg.data is of type *bytes* and contains the **raw data** of the *function call*. 

By using *msg.data*, you can access the raw *byte* data passed to the *function* and perform parsing and processing operations.

<aside>
💡 When you call a *function* in a *contract*, you can pass additional data along with the Ether value and listed parameters with *low-level call*. This data can be of any type, including *strings, byte arrays*, and more. By using msg.data, you can access this passed data and execute corresponding logic within the *contract*.

</aside>

- Metaphor
    
    Imagine msg.data in Solidity as the content of a letter sent to you. It contains all the details and instructions, like the sender's address and the message itself, allowing you to understand and act upon the information enclosed.
    
- Real Use Case
    
    This is commonly used, for example in [***Context***](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/utils/Address.sol#L105) , we see that
    
    ```solidity
    abstract contract Context {
        function _msgSender() internal view virtual returns (address) {
            return msg.sender;
        }
    
        function _msgData() internal view virtual returns (bytes calldata) {
            return msg.data;
        }
    }
    ```
    

### Documentation

```solidity
//We are using msg.data to retrieve the original data when this function was called and assigning the value to the variable ***data***.
bytes memory data = msg.data;
```

In Solidity, we can use the global variable `msg.data` to access the **raw data** of a *function call*.

### FAQ

- When to use `msg.data`?
    
    `msg.data` is usually used within the fallback function, to check the exact function call data made by the user. 
    
    ```solidity
    fallback() external payable {
      // Here, you have access to msg.data, which contains the raw
      // bytes sent to the contract. You can do something with these
      // bytes if you like, or ignore them.
      if (msg.data.length > 0) {
        // Custom handling of the data...
      }
    }
    ```
    

# Example/Example

```solidity
pragma solidity ^0.8.0;

contract DataContract {
  bytes data;
  function process() public returns (bytes memory) {
    data = msg.data;

    // ...

    return data;
  }
}
```