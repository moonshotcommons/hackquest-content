# Content/Content

### Concept

Local variables are *variables* defined in *functions*. They are temporary containers that are used to store values within a specific section (function) of a program.

- Metaphor
    
    Imagine you’re making your cake again. After adding sugar, somehow you will need to remember that you’ve added sugar already. Although, this information is not important after you’re done making your cake. But, for now, it’s important. This information is **temporary**, and should be stored as a **local** variable. 
    
- Real Use Case
    
    ```solidity
    function transfer(address to, uint256 value) public virtual returns (bool) {
        address owner = _msgSender();
        _transfer(owner, to, value);
        return true;
    }
    ```
    
    The ***[transfer](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/1523a4f071f101d4bcbffcd4b87dd1b03080ec26/contracts/token/ERC20/ERC20.sol#L118-L122)*** function in ERC20 can transfer tokens from the owner to another address. It has a local variable owner to represent the caller address that is only used in this function.
    

### Documentation

```solidity
contract ContractName {
  function example() {
    int a;//this is a local variable 
    a = 3;
  }
}
```

To define a local variable, it’s the same process as *state variables*, only it’s defined inside a *function*. 

### FAQ

- Local Variable VS State Variable?
    
    Local Variable is cheap, but it’s temporary. State variable is expensive but it’s permanent. 
    
    Therefore, these two are actually easy to distinguish: you use state variables for all the information that you want to keep record, and local variables for the rest. 
    
    However, there’re also some variables you could only define as state variables, like mapping, but these are special cases
    
- Why does not ERC20 contract in Oppenzeppelin use `msg.sender` directly?
    
    OpenZeppelin's ERC20 contracts don't always use msg.sender directly because they often require more complex access control, ownership management, and security considerations that go beyond the simple use of the msg.sender variable. This allows for better customization and security in different scenarios.
    
    If the contract is called by another contract and there’s some complex proxy usages involved, msg.sender is not enough. Oppenzeppelin leaves space for upgrades. 
    

# Example/Example

```solidity
pragma solidity ^0.8.0;
contract Example {
  uint c;
  function getResult() public returns(uint){
    uint a = 1; // local variable
    uint b = 2;
    uint result = a + b;
    c = result; // this is not a local variable
    return result; //access the local variable
  }
}
```
