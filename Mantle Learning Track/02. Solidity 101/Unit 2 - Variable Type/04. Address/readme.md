# Content/Content

### Concept

 An address is an identifier for an **account** or a *smart contract* on the Ethereum blockchain. 

It’s a number in hexadecimal. 

```solidity
//0x means the following number is in hexadecimal 
address address1 = 0x35701d003AF0e05D539c6c71bF9421728426b8A0;
```

- Metaphor
    
    It is like a unique username or account number in your bank. It helps to identify and interact with individual users or entities.
    
- Real Use Case
    
    In the [ERC20](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/8186c07a83c09046c6fbaa90a035ee47e4d7d785/contracts/token/ERC20/ERC20.sol#L118) transfer function, the `address` data type is used to represent recipient addresses.
    
    ```solidity
    function transfer(address to, uint256 value) public virtual returns (bool) {
        address owner = _msgSender();
        _transfer(owner, to, value);
        return true;
    }
    ```
    
    Also when you register your wallet, you’re assigned a **unique** account address. 
    

### Documentation

```solidity
// Definition
address address1 = 0x35701d003AF0e05D539c6c71bF9421728426b8A0;
//This is a conversion from a hexadecimal number to a valid address
address address2 = address(0x123)//address2 = 0x0000000000000000000000000000000000000123
```

To define an address, we have a *variable* name after the type.

### FAQ

- What are the different *account addresses* ****and *contract addresses*?
    
    An address could be one of these two things: account *address* or contract *address*.
    
    **Account address**
    
    It’s created to receive or send money by a user, a.k.a. a **user-controlled** *address*. This is also referred to as a wallet. Check out Metamask if you’re not familiar with this concept. 
    
    **Contract address**
    
    In contrast with **account address**, **contract address** is controlled by a contract (program). When you put your contract on Ethereum, you put it to an address on Ethereum. And this identifier is how people interact with you.
    
- What is address.balance and address.transfer?
    
    These two are the built in *functions* of *address*. Built in function means Solidity created these functions for all variables in this type and you can use it directly. 
    
     **Balance**
    
    ***balance*** allows contracts to check how much balance is left in one *address* .
    
    ```solidity
    // Balance is in uint because it can never be negative 
    uint balance = address1.balance;
    ```
    
    **Transfer**
    
    ***transfer*** allows contracts to transfer money from itself to another address, where the amount transferred is in unit *Wei*, 1 Eth = 10^18 *Wei* .
    
    ```solidity
    // transfer 5 Wei from this contract to address1 
    address1.transfer(5);
    ```
    

# Example/Example

```solidity
pragma solidity ^0.8.0;

contract AddressArray {
  address payable add = payable(0x5B38Da6a701c568545dCfcB03FcB875f56beddC4);
  address b = add;
  uint balance = b.balance;
}
```
