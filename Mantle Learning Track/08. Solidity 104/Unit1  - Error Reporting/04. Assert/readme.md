# Content/Content

### Concept

A while ago, we learned about two error handling mechanisms, `require` and `revert`, and now we will introduce the third error handling syntax `assert`

`Assert`, similar to `require`, checks if a certain condition is met. If not, it terminates the execution of the *function* and undoes all changes. 

- Metaphor
    
    Imagine you're building a toy car with LEGO bricks. The wheels are crucial – without them, it's not a car. An `assert` in Solidity is like a final check to make sure the wheels are attached. If the wheels aren't on, the toy car build completely falls apart and stops.
    
- Real Use Case
    
    In Solidity, the `assert()` is commonly used for internal error checks. In the provided *smart contract's* ***withdraw** function*, there's a segment that showcases this:
    
    ```solidity
    // Double-check the subtraction logic
    assert(balances[msg.sender] == expectedNewBalance);
    
    ```
    
    This `assert` checks that after deducting the withdrawal amount from `balances[msg.sender]`, the resulting balance is indeed the expected value (***expectedNewBalance***). If the resulting value doesn't match the expected value for any reason, the `assert` will fail, and the transaction will be *reverted*.
    
    For example, we‘re adding two large numbers, and we want to make sure that their sum is not bigger than the `uint256` type can take.
    
    ```solidity
    uint256 c = a + b; 
    assert(c > b);
    ```
    

### Documentation

In Solidity, the `assert` keyword is used to check for internal *errors* and constraints that should never be false assuming the code is correct.

```solidity
// Using `assert` to ensure a user's balance is less than the total supply. 
// If a user's balance exceeds the total supply, it indicates a fundamental bug in the system.
assert(balance[msg.user] < totalSupply);
```

### FAQ

- What happens to the state of a contract when an assert condition fails?
    
    When an `assert` fails, it triggers a revert operation, which undoes all state changes made during the execution of the failing transaction. This ensures that the contract remains in a consistent state even after encountering a critical internal error.
    
- ****How does the behavior of assert differ from require in Solidity?
    
    **assert**: Used to handle invariants and internal errors. If an `assert` fails, all gas is consumed, signaling that there's a deeper issue with the *contract's* logic.
    
    **require**: Used to validate external inputs and conditions. If a `require` fails, the remaining gas is refunded to the caller. It's generally used for standard operational checks, like ensuring valid inputs or sufficient balances.
    

# Example/Example

```solidity
pragma solidity 0.6.0;

contract Bank {
  mapping(address => uint256) balanceOf;

  function deposit(uint256 amount) public payable {
    //using require to check parameters
    require(msg.value == amount, "Deposit amount must be equal to the sent value");
    uint256 oldBalance = balanceOf[msg.sender];
    balanceOf[msg.sender] += amount;

    //using assert to check the correctness of code execution(here to prevent overflow)
    assert(balanceOf[msg.sender] > oldBalance);
  }

  function withdraw(uint256 amount) public {
    //Using revert statements to handle multiple potential error scenarios in if-else statements.
    if(amount <= 0) {
      revert("Invalid withdrawal amount");
    }else if(balanceOf[msg.sender] < amount) {
      revert("Insufficient balance for withdrawal");
    }
    payable(msg.sender).transfer(amount);
    uint256 oldBalance = balanceOf[msg.sender];
    balanceOf[msg.sender] -= amount;

    //using assert to check the correctness of code execution(here to prevent overflow)
    assert(balanceOf[msg.sender] >= oldBalance);
  }
}
```
