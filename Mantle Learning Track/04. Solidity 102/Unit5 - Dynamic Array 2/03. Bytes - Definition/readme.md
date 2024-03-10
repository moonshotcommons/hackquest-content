# Content/Content

### Concept

In the previous section, we learned about the access operation on dynamic arrays in Solidity. In this section, we will continue to discuss a special type of array: bytes.

Bytes is a dynamically sized byte array in Solidity. 

- Real Use Case
    
    In [Address.sol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/181d518609a9f006fcb97af63e6952e603cf100e/contracts/utils/Address.sol#L95), bytes are used to process more general data. When we making general function calls, it’s hard to predict the return types/data. In this case we will use bytes to receive the data and pass it somewhere else for processing. 
    
    ```cpp
    /**
     * @dev Same as {xref-Address-functionCall-address-bytes-}[`functionCall`],
     * but performing a static call.
     */
    function functionStaticCall(address target, bytes memory data) internal view returns (bytes memory) {
        (bool success, bytes memory returndata) = target.staticcall(data);
        return verifyCallResultFromTarget(target, success, returndata);
    }
    ```
    

### Documentation

You can define a bytes *variable* by using the bytes keyword followed by the *variable* name.

```solidity
//bytes variableName;
bytes data;
```

In terms of syntax, it differs from other dynamic arrays in that it does not require square brackets when defining it.

### FAQ

- How can you quickly convert between bytes and string types?
    
    Variables of type bytes and string are special arrays. 
    
    - **‍**A string can be quickly converted to a byte array using bytes(string).
    - A byte array could be quickly converted to a string using string(bytes) .
    
    ```solidity
    string name = "abcdef";
    bytes stringArr = bytes(name);
    name = string(stringArr);
    ```
    

# Example/Example

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract BytesExample {
    bytes data;
}
```
