# Content/Content

### Concept

Every reference type has an additional annotation, the data location, about where the data is stored. There are three options - storage, memory, and calldata.  

First, we introduce the storage location. Data stored in this location is persisted on the Ethereum blockchain. This location is used to store long-term state variables in contracts.

- Metaphor
    
    Think of storage as the hard drive of a computer. When you save a file to the hard drive, it stays there even if you turn off the computer. You can come back days, months, or even years later, turn on the computer, and the file will still be there, unchanged. 
    
    Similarly, data in the storage location of a Solidity contract is permanent and remains on the blockchain even after the transaction that created or modified it is over. Once written, it can be accessed or modified in future transactions, but it never disappears. 
    
- Real Use Case
    
    The ERC20 *contract* is a template for creating fungible tokens on the Ethereum blockchain, standardizing the *functions* for transferring and managing tokens. 
    
    It mainly relies on two mappings, [***_balances***](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/token/ERC20/ERC20.sol#L39C1-L39C59) and [***_allowances***](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/token/ERC20/ERC20.sol#L41C1-L41C89), stored in Ethereum's storage *memory location*, ensuring that the information remains on the blockchain even after *contract* execution.
    
    1. **_balances Mapping**: This *mapping* stores the number of tokens owned by each *address*. When users send or receive tokens, the *contract* updates the ***_balances*** with the new balances.
        
        ```solidity
        mapping(address account => uint256) private _balances;
        ```
        
    2. **_allowances Mapping**: This *mapping* records the amount of tokens that an *address* has allowed another *address* to transfer on its behalf. When a user transfers tokens on behalf of another user, the contract reduces the allowance in the ***_allowances*** and updates the ***_balances*** .
        
        ```solidity
        mapping(address account => mapping(address spender => uint256)) private _allowances;
        ```
        
    
    Both *mappings* use the storage *memory location*, which provides a permanent record of token ownership and transfer permissions on the Ethereum blockchain.
    

### Documentation

To put a variable in storage , you need to define it as a state variable, outside of *functions* .

```solidity
string str; //this string state variable is in storage
function a() {
  //function body
}
```

### FAQ

- When to use Storage?
    
    Anything that you would like to store permanently on the Ethereum Blockchain should be stored in storage. Also, some data types can only be stored in storage. For example, all *mappings* are in *storage*.
    
- In terms of gas costs, is it more expensive to store data in the storage location on the Ethereum blockchain?
    
    Storing data in the *storage* location on the Ethereum blockchain is more expensive in terms of gas costs compared to other locations. This is because data in the *storage* location is persisted on the blockchain, ensuring its permanence and accessibility over time.
    
    ![IMG_FED1178E6000-1.jpeg](./img/1-1.jpeg)
    

# Example/Example

```solidity
pragma solidity ^0.8.4;

contract storageExample {
  string name = "hello"; //this string state variable is in storage
  function update() public {
    name = "hello~";
  }
}
```
