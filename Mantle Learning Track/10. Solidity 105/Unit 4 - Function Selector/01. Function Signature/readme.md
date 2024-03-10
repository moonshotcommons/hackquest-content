# Content/Content

### Concept

A function signature is a unique identifier for a *function.* It’s usually used to get function selector (which will be explained in the next lesson), and function selector is used to identify function calls. 

- Metaphor
    
    A *function signature* in programming is like a unique fingerprint for a person, containing specific patterns and characteristics that identify the function's name and parameter types, allowing others to recognize and interact with it effectively.
    
- Real Use Case
    
    In [***IERC1155Receiver***](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/token/ERC1155/IERC1155Receiver.sol#L18), as written in the comments, we have that ***onERC1155Received*** *function* which is defined to return the first four bytes of its function signature. 
    
    ```solidity
    /**
     * @dev Handles the receipt of a single ERC1155 token type. This function is
     * called at the end of a `safeTransferFrom` after the balance has been updated.
     *
     * NOTE: To accept the transfer, this must return
     * `bytes4(keccak256("onERC1155Received(address,address,uint256,uint256,bytes)"))`
     * (i.e. 0xf23a6e61, or its own function selector).
     *
     * @param operator The address which initiated the transfer (i.e. msg.sender)
     * @param from The address which previously owned the token
     * @param id The ID of the token being transferred
     * @param value The amount of tokens being transferred
     * @param data Additional data with no specified format
     * @return `bytes4(keccak256("onERC1155Received(address,address,uint256,uint256,bytes)"))` if transfer is allowed
     */
    function onERC1155Received(
        address operator,
        address from,
        uint256 id,
        uint256 value,
        bytes calldata data
    ) external returns (bytes4);
    ```
    

### Documentation

Function signature is defined as the canonical expression of the basic prototype, i.e. the *function name* with the parenthesized list of *parameter types*.

```solidity
//function signature: "hello(uint256,address,bool)"
function hello(uint256 a, address b, bool c) {...}
```

### FAQ

- Could we have the same function signature for two functions?
    
    It’s impossible in the same contract because Solidity uses the first four bytes of the hash of the function signature to identify the function called. If two functions have the same signature, Solidity won’t be able to decide which one to call. 
    

# Example/Example

```solidity
pragma solidity ^0.8.0;

contract FunctionSignature {
  function dosome(uint256 num, string memory text) public pure returns (string memory signature) {
    // Calculate the function signature.
    signature = "dosome(uint256,string)";
  }
}
```