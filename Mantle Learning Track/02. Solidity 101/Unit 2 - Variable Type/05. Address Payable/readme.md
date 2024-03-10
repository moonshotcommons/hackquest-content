# Content/Content

### Concept

The `address payable` type in Solidity is used to represent Ethereum *addresses* that you want to send Ether to.

- Metaphor
    
    Imagine a shopping mall with two kinds of stores: showrooms where you cannot make purchases and fully plugged stores where you can see and buy.
    
    - Regular address: This is like a showroom where you could see but cannot send money to it
    - Payable address: This is a fully plugged store where you can see and buy things (send Ether to it)
- Real Use Case
    
    In the OpenZeppelin's [ERC2771Forwarder](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/8186c07a83c09046c6fbaa90a035ee47e4d7d785/contracts/metatx/ERC2771Forwarder.sol#L162-L165) contract, the parameter ***refundReceiver*** is defined as `payable`, which also means that we could send Ether to this ***refundReceiver** address* in this ***ERC2771Forwarder*** *contract*.
    
    ```solidity
    function executeBatch(
        ForwardRequestData[] calldata requests,
        address payable refundReceiver
    ) public payable virtual {
        ...
    }
    ```
    

### Documentation

```solidity
address payable add = payable(address(0x123));
```

To define an address payable *variable*, we use the keyword `address payable`. 

### FAQ

- When should we define address payable?
    
    If we want to transfer money Ether our account to this account, then we should mark it address payable. 
    
- How to convert an address from a regular address to a payable address?
    
    To convert from address payable to address, we don’t need to do anything —  we can just use address payable variables as address type variables, this is called implicit conversion. 
    
    However, to convert from address to address payable, we need explicit conversion, using the keyword payable. 
    
    ```solidity
    address payable add = payable(0x5B38Da6a701c568545dCfcB03FcB875f56beddC4);
    address b = add; //implicit converting from address payable to address
    address payable d = payable(b); // explicit conversion with payable()
    ```
    
- How to transfer Ether to a payable address?
    
    ***transfer*** allows contracts to transfer money from itself to another address, where the amount transferred is in unit Wei, 1 Eth = 10^18 Wei 
    
    In Solidity, the ***transfer*** method allows smart contracts to send Ether from their own account to another address. This transfer is specified in terms of "Wei", the smallest denomination of Ether, where 1 Ether equals 1,000,000,000,000,000,000 Wei (10^18 Wei).
    
    Example: Suppose you want to transfer 5 Wei from the current contract to an address ***transfer1***. You would use the code `address1.transfer(5);` to execute this transfer. This command deducts the specified amount from the contract's balance and sends it to ***transfer1***.
    
    ```solidity
    //transfer 5 Wei from this contract to address1 
    address1.transfer(5);
    ```
    

# Example/Example

```solidity
pragma solidity ^0.8.0;

contract AddressArray {
  address payable add = payable(0x5B38Da6a701c568545dCfcB03FcB875f56beddC4);
  address b = add;
  uint balance = b.balance;
	//We will make the function payable so we could send Ether
	//to this function and this function call transfer to send
	//Ether to the address
  function trans() public payable {
    //this transfers 10 Wei to address b from the current contract 
    add.transfer(10);
  }
}
```
