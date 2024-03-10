# Content/Content

### Concept

Starting from Solidity 0.8.x, developers have the option to define *custom errors* with specific *parameters*. These *errors* can then be used with the `revert` statement to signal structured error conditions.

- Real Use Case
    
    In [draft-IERC6093.sol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/181d518609a9f006fcb97af63e6952e603cf100e/contracts/interfaces/draft-IERC6093.sol#L17C1-L27C50), we defined two *errors* 
    
    ```cpp
    /**
     * @dev Indicates a failure with the token `sender`. Used in transfers.
     * @param sender Address whose tokens are being transferred.
     */
    error ERC20InvalidSender(address sender);
    
    /**
     * @dev Indicates a failure with the token `receiver`. Used in transfers.
     * @param receiver Address to which tokens are being transferred.
     */
    error ERC20InvalidReceiver(address receiver);
    ```
    
    In [ERC20.sol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/181d518609a9f006fcb97af63e6952e603cf100e/contracts/token/ERC20/ERC20.sol#L171C1-L179C6), we use `revert` to stop execution, undo all changes, and report the error to the function caller.
    
    ```cpp
    function _transfer(address from, address to, uint256 value) internal {
        if (from == address(0)) {
            revert ERC20InvalidSender(address(0));
        }
        if (to == address(0)) {
            revert ERC20InvalidReceiver(address(0));
        }
        _update(from, to, value);
    }
    ```
    

### Documentation

You can use the `revert` statement to export custom error types.

```solidity
// Custom error type.
error MyCustomError(string message);
// Checks if value exceeds 100 and throws error if so.
function process(uint256 value) public pure {
  if (value > 100) {
    revert MyCustomError("Value exceeds limit");
  }
}
```

### FAQ

- What are the advantages and disadvantages of revert error？
    
    **Advantage**: Offers structured error handling which is gas-efficient compared to *strings*. Also, provides a more detailed context of the *error*, allowing for better off-chain handling.
    
    **Disadvantage**: Slightly more complex than a simple string message, but the benefits usually outweigh this added complexity.
    

# Example/Example

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Bank {
  mapping(address => uint) private balances;

  //Custom Error Type InsufficientFunds
  error InsufficientFunds(uint requested, uint available);
  
  function deposit() public payable {
    balances[msg.sender] += msg.value;
  }

  function withdraw(uint amount) public {
    if (amount > balances[msg.sender]) {
      revert InsufficientFunds(amount, balances[msg.sender]);
    }
    balances[msg.sender] -= amount;
    payable(msg.sender).transfer(amount);
  }

  function getBalance(address account) public view returns (uint) {
    return balances[account];
  }
}
```
