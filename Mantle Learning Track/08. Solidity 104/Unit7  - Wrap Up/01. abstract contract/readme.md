# Content/Content

### Concept

So far, we have learned about two special *contracts*: library and interface. In this section, we will learn about the third type of special *contract*: abstract contract.

An *abstract contract* cannot be instantiated but serves as a base for other *contracts*. It defines *functions*, *variables*, and common *functionalities*.

- Metaphor
    
    For example, you're building a house with different rooms. Each room has common features like walls, doors, and windows, but can also have its own unique design and purpose.
    
    ```solidity
    // Abstract contract representing the common blueprint for rooms in a house
    abstract contract AbstractRoom {
      uint256 public numberOfWalls;
      bool public hasDoors;
      bool public hasWindows;
    
      // Abstract method to be implemented by concrete contracts
      function decorate() external virtual;
    }
    
    // Concrete contract for a bedroom
    contract Bedroom is AbstractRoom {
      constructor() {
        numberOfWalls = 4;
        hasDoors = true;
        hasWindows = true;
      }
    
      // Implementation of the decorate method specific to a bedroom
      function decorate() external override {
        // Add bedroom-specific decorations
      }
    }
    ```
    
- Real Use Case
    
    In the [ERC20](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/token/ERC20/ERC20.sol#L38) contract given by OpenZeppelin, [ERC20](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/token/ERC20/ERC20.sol#L38) is defined as an abstract contract, so the *contract* cannot be *instantiated*.
    
    ```solidity
    abstract contract ERC20 is Context, IERC20, IERC20Metadata, IERC20Errors {
    ```
    

### Documentation

We can define an *abstract contract* using the `abstract` keyword.

```solidity
//defined an abstract contract named **ContractA**.
abstract contract ContractA { }
```

### FAQ

- What is the main difference between abstract contracts and interfaces in terms of variables and implementations in Solidity?
    
    *Abstract contracts* can have **variables** and **implementations**, while *interfaces* only have **function signatures**.
    
- What is the only difference between regular contracts and abstract contracts in terms of deployment in Solidity?
    
    The only difference is that regular *contracts* can be **deployed**, whereas abstract contracts cannot.
    

# Example/Example

```solidity
// Abstract contract
abstract contract Animal {
  // Abstract contracts can have variable definitions
  string public name;
  bool public hasEaten;

  event EatEvent(string name);
  // Abstract contracts can also have constructors
  constructor(string memory _name) {
    name = _name;
  }

  function speak() public virtual returns (string memory);

  function eat() public virtual {
    // Abstract contracts can include implementations
    // The specific function can be overridden in child contracts
    hasEaten = true;
  }
}

// Contract implementing the abstract contract
contract Cat is Animal {
  constructor(string memory _name) Animal(_name) {}

  function speak() public override returns (string memory) {
    return "Meow";
  }

  function eat() public override {
    // Override the eat function from the abstract contract
    // Provide specific eating function for cats
    super.eat();
    emit EatEvent(name);
    // Perform other eating operations for cats
  }
}
```
