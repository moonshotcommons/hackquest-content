# Content/Content

### Concept

In the previous section, we learned about the `msg.value` *global variable*. In this section, we will learn about how to pay ETH to another *function* inside a *function*.

When you make a *function call* in a *smart contract*, you can also send Ether (ETH) at the same time. This lets you both transfer value (in the form of ETH) and interact with the contract in one step.

- Metaphor
    
    *Paying ETH* with a function call is like dropping coins into a vending machine to select a product – you initiate an action (calling the function) while also providing payment (sending Ether) to receive the desired outcome.
    
- Real Use Case
    
    In OpenZepplin's [***Address***](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/utils/Address.sol#L83) contract, the `address.call{value :}` method is used to attach ETH while calling the function.
    
    ```solidity
    function functionCallWithValue(address target, bytes memory data, uint256 value) internal returns (bytes memory) {
        ...
        (bool success, bytes memory returndata) = target.call{value: value}(data);
        ...
    }
    ```
    

### Documentation

To send ETH while making the *function* call, we just need to add `{}` ****between the name of the `function` and its `parameters`. 

The unit of Ether we transferred is represented in Wei, while 1 Ether = $10^{18}$ Wei. 

```solidity
deposit{value: 5}();
```

### FAQ

- What is the minimum/maximum ETH I can pay?
    
    **Minimum**: You must have enough ETH to cover both the transaction fee and the amount you're sending. The smallest unit of ETH is called a "Wei," which is 10^-18 ETH.
    
    **Maximum**: Limited by the balance in your wallet, minus transaction fees. The largest amount of ETH that can theoretically be held in a single account is 2^256 - 1 wei, an astronomically large number.
    
- Does my ETH payment have to be a function call?
    
    Sending Ether (ETH) involves creating a transaction, which can be considered a type of function call, either explicitly to a contract's functions or implicitly to a contract's fallback function or to an externally owned Ethereum address (EOA).
    
- From where is the ETH paid when calling a payable function in a smart contract?
    
    When you call a payable function in a smart contract, the ETH is paid from the account (either an Externally Owned Account or another contract) that initiates the call. This account is referred to as `msg.sender` in Solidity. It's important that `msg.sender` has enough ETH to cover the transaction, including any gas fees.
    

# Example/Example

```solidity
pragma solidity ^0.8.0;

contract Bank {
  mapping(address => uint256) public balances;

  function deposit() public payable {
    balances[msg.sender] += msg.value;
  }
}

contract User {
  Bank public bank;

  constructor(address _bankAddress) {
    bank = Bank(_bankAddress);
  }

  function depositToBank() public payable {
    bank.deposit{value: 5}();
  }
}
```
