# Content/Content

### Concept

A function selector refers to the **first 4 bytes** of the hash of a function signature, used to uniquely identify a *function* within a contract. 

<aside>
💡 All *function calls* are identified by function selectors in Solidity.

</aside>

- Metaphor
    
    A function selector in Solidity is like the code of a book on a library shelf, a concise code that encapsulates the function's identity and purpose, making it easy to locate and retrieve the right book (function) from a vast collection (contract).
    
- Real Use Case
    
    In our previous use case, we see that ***onERC1155Received*** actually requires the *function* to return its own function selector to accept the transfer. 
    
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

We could either manually calculate the selector of a *function* or directly call `functionName.selector` 

```solidity
function myFunction(address a, uint b, bytes c) public {...}

bytes4 selector = bytes4(keccak256("myFunction(address,uint256,bytes)"));
bytes4 selector = myFunction.selector;
```

### FAQ

- When do we want to use function selector?
    
    The `function selector` in Solidity is used when **making low-level calls** **to external contracts** and **implementing interfaces**. It helps specify the desired `function` to be called in `contract` interactions and ensures proper `interface` implementation.
    

# Example/Example

```solidity
pragma solidity ^0.8.0;

contract FunctionSignature {
  function dosome(uint256 num, string memory text) public pure returns (bytes4 selector1, bytes4 selector) {
    selector = bytes4(keccak256("dosome(uint256,string)"));
    selector1 = this.dosome.selector;
  }
}
```