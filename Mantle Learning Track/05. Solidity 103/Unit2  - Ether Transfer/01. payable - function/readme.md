# Content/Content

### Concept

In Solidity, payable is a modifier that can be applied to *functions* or *addresses*. When *payable* is added to a *function*, that *function* is able to receive Ether (ETH) during a transaction. If a *function* doesn't have the *payable* modifier, it will reject any incoming Ether.

```solidity
contract MyContract {
  function acceptPayment() public payable {
    // Function body
  }
}
```

- Metaphor
    
    Let's imagine a simple vending machine that sells digital art pieces (NFTs).
    
    The *payable function* is like the coin slot on the vending machine. It's the part that accepts your money (Ether) so you can buy an art piece (NFT). If there was no coin slot (*function* without *payable*), you couldn't put your money in, and you wouldn't be able to buy any art.
    
    So, if you want your *smart contract* to be able to receive Ether (like a vending machine accepting coins), you use a *payable* function.
    
- Real Use Case
    
    In OpenZepplin's ***[ERC2771Forwarder](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/metatx/ERC2771Forwarder.sol#L162C27-L162C27)*** contract, ***executeBatch*** is decorated with *payable*, which proves that the function may need to pass in ETH for calling.
    
    ```solidity
    function executeBatch(
        ForwardRequestData[] calldata requests,
        address payable refundReceiver
    ) public payable virtual {
    ```
    

### Documentation

A *payable* function is declared like any other function but with the `payable` keyword.

```solidity
function depositFunds() public payable {
  // Code to execute when Ether is sent
}
```

### FAQ

- What’s the difference between a payable function and a payable address?
    
    A *payable function* is a function within a contract that can receive Ether, while a payable address is an Ethereum address capable of receiving Ether directly. The terms refer to different aspects of handling Ether transactions within the Ethereum ecosystem.
    

# Example/Example

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.17;

contract PayableExample{
  function depositFunds() public payable { }

  function getBalance() public view returns (uint) {
    return address(this).balance;
  }
}
```
