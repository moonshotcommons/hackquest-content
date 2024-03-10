# Content/Content

### Concept

Previously, we learned about the exception handling mechanism —— `revert`, which can *return* some error information. Here, we will learn a type — `error`, specifically designed for this error information. 

- Metaphor
    
    `Error` is like a struct. In a *struct*, you group different properties together; in *error*, you group different error messages together. 
    
    ![error.jpg](./img/2-1.jpg)
    
- Real Use Case
    
    In [ERC20](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/token/ERC20/ERC20.sol#L51) *contracts*, sometimes users would like to allow other address to spend their account balance. In this case, we will have a *function* called ***decreaseAllowance*** which the caller could use to decrease the amount granted to the ‘spender’. 
    
    To implement the ***decreaseAllowance** function* in an ERC20 *smart contract*, you must first have an allowance mapping that keeps track of allowances given by token holders to other *addresses*.
    
    The ***ERC20FailedDecreaseAllowance*** error might be triggered in cases where the operation to decrease the allowance fails due to.
    
    Let's implement the ***decreaseAllowance** function*, incorporating the ***ERC20FailedDecreaseAllowance*** error:
    
    ```jsx
    error ERC20FailedDecreaseAllowance(address spender, uint256 currentAllowance, uint256 requestedDecrease);
    ```
    

### Documentation

In Solidity, define the *error* type using the keyword `error`, followed by its parameter.

```solidity
error UnauthorizedAccess();
error InsufficientFunds(uint256 balance, uint256 withdrawalAmount);

function withdraw(uint256 amount) public {
    if (msg.sender != owner) {
        revert UnauthorizedAccess();
    }
    if (balance[msg.sender] < amount) {
        revert InsufficientFunds(balance[msg.sender], amount);
    }
    // ... rest of the function ...
}

```

In this example, two custom errors are defined: ***UnauthorizedAccess*** and ***InsufficientFunds***. The ***withdraw** function* then uses these errors with the `revert` statement to indicate specific error conditions.

### FAQ

- Why is the error feature needed in Solidity?
    
    The `error` feature in Solidity provides a structured way to signal error conditions in *smart contracts*. Before its introduction in Solidity 0.8.x, developers relied on string messages with the `revert` statement to indicate errors, which was not only gas-inefficient due to the storage and execution costs associated with strings but also lacked a standardized structure. The `error` feature *addresses* these issues by allowing developers to define structured error types with specific parameters, leading to clearer, more gas-efficient, and standardized error handling.
    
- When should developers use the error feature in Solidity?
    
    Developers should use the `error` feature whenever they need to indicate an error condition in a *smart contract* *function*. Common scenarios include **validating function arguments**, **enforcing access controls**, **ensuring state consistency**, or **checking contract invariants**. Any time a *function* cannot proceed as expected and needs to revert the transaction, an appropriate error can be used to provide clear information about the reason for the reversion.
    

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
      //it will be explained in the next lessons
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
