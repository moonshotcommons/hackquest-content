# Content/Content

### Concept

require checks if a certain *condition* is satisfied in the code.

If not, then it reports an error message and terminates the execution. The error message is optional.

- Metaphor
    
    The require statement in Solidity is like a security checkpoint at the entrance of a restricted area, ensuring that only individuals meeting certain conditions can proceed further into the area. If the conditions aren't met, access is denied and the process is halted.
    
- Real Use Case
    
    ```solidity
    require(liquidity > 0, 'UniswapV2: INSUFFICIENT_LIQUIDITY_MINTED');
    ```
    
    In the ***[mint](https://github.com/Uniswap/v2-core/blob/ee547b17853e71ed4e0101ccfd52e70d5acded58/contracts/UniswapV2Pair.sol#L125)*** function in the ***UniswapV2Pair*** contract, the require statement checks if the variable ***liquidity*** is greater than zero. If ***liquidity*** is not greater than zero, the function execution will halt, and an error message *'UniswapV2: INSUFFICIENT_LIQUIDITY_MINTED'* will be provided as the reason for the revert.
    
    The purpose of this *require* statement is to ensure that the minting operation is valid and meaningful. In the context of a decentralized exchange like Uniswap, the ***mint*** function is used to create liquidity tokens when users provide liquidity to a trading pair. The amount of liquidity tokens to be minted depends on the amount of tokens provided and the current reserves of the trading pair.
    

### Documentation

```solidity
require(recipient != address(0), "Recipient address cannot be zero");
```

To check on the *condition*, we use the keyword `require`, then follow by the *condition*, and a message to report error if the *condition* is not satisfied. 

### FAQ

- Why do we need require?
    
    **Error processing** is an important section in every piece of code. We all expect things to go in certain ways, but the truth is they don’t, in many cases. 
    
    For a computer to work properly, we need to define every edge cases, otherwise it will stuck. require is defining an edge case and instructing the computer what to do under such edge cases. 
    
     
    

# Example/Example

```solidity
pragma solidity ^0.8.4;
contract VendingMachine {
  address a = address(0x123);
  function buy(uint amount) public payable {
    require(
      //we will explain msg.sender in next lesson
      a == msg.sender,
      "Not authorized."
    );
    // Execute the purchase.
  }
}
```
