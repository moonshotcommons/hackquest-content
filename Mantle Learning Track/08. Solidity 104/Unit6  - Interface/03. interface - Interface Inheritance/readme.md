# Content/Content

### Concept

In the previous lessons, we learned about defining *interfaces*. In this section, we will learn about interface inheritance.

Both *interface* and *contract* could *inherit* from *interface*. *Contract inheriting* an *interface* must implement all the *functions* in the *interface*. Interface ***A*** inhering an interface ***B*** copies the code from ***B*** to ***A***, like contract ***A*** inheriting contract ***B***.

- Metaphor
    
    For example, you are a band manager, you ensure a band can play various styles like rock or jazz before signing, without concerning their techniques.
    
    ```solidity
    // This is your "contract" with the band.
    interface IBand {
      function performRock() external;
    }
    
    // The band signs your contract (inherits your interface) and promises to provide these capabilities.
    contract Band is IBand {
      function performRock() external override {
        // Implementation of rock performance...
      }
    }
    ```
    
- Real Use Case
    
    In the implementation of ***UniswapV3Pool***, the ***[IUniswapV3Pool](https://github.com/Uniswap/v3-core/blob/d8b1c635c275d2a9450bd6a78f3fa2484fef73eb/contracts/UniswapV3Pool.sol#L30C1-L30C59)** interface* is *inherited*, which means that it contains all *functions* defined in the *interface*.
    
    ```solidity
    contract UniswapV3Pool is IUniswapV3Pool, NoDelegateCall {
    ```
    

### Documentation

When a *contract* in Solidity *inherits* an interface using the `is` keyword, it's important to understand that the *contract* is not *inheriting* any implemented functionality. Instead, the *contract inherits* a set of function signatures that it must then implement.

```solidity
//we define a contract named **ContractA** and inherit the **InterfaceA** interface,
//which means we must implement all the functions specified in **InterfaceA**.
pragma solidity ^0.8.0;

interface InterfaceA {
    function doSomething(uint256 value) external returns (uint256);
}

contract ContractA is InterfaceA {
    uint256 private data;

    // Constructor to initialize data
    constructor() {
        data = 0;
    }

    // Implementing the doSomething function from InterfaceA
    function doSomething(uint256 value) external override returns (uint256) {
        data += value;
        return data;
    }
}
```

### FAQ

- Why do we need to inherit interfaces?
    
    Inheriting from an *interface* compels a *contract* to implement all *functions*, ensuring standardized, predictable interactions and streamlined, manageable code through abstraction.
    
- What are the key differences between contract inheritance and interface inheritance in Solidity?
    
    Unlike *contact inheritance* which gives the *child contract* all the *functionalities* and *variables* in the *parent contract*, interface inheritance is completely different —— it gives you no *functionalities* nor *variables* while defining a set of *functions* waiting to be implemented in the *child contract*. 
    

# Example/Example

```solidity
// Interface: Transferable Interface
interface Transferable {
  function deposit(uint256 amount) external returns (bool);
  function transfer(address recipient, uint256 amount) external returns (bool);
  function getBalance() external view returns (uint256);
}

// Contract: BankAccount
// Inherits from the Transferable interface, which means our contract must include the transfer and getBalance functions.
contract BankAccount is Transferable {
  mapping(address => uint256) private balances;

  // Implement the deposit function
  function deposit(uint256 amount) external override returns (bool) {
    balances[msg.sender] += amount;
    return true;
  }

  // Implement the transfer function
  function transfer(address recipient, uint256 amount) external override returns (bool) {
    require(balances[msg.sender] >= amount, "Insufficient balance");
    balances[msg.sender] -= amount;
    balances[recipient] += amount;
    return true;
  }

  // Implement the getBalance function
  function getBalance() external view override returns (uint256) {
    return balances[msg.sender];
  }
}
```
