# Content/Content

### Concept

In this section, we will learn about function overriding in inheritance. *Function overriding* allows a *child contract* to **replace** the implementation of a function *inherited* from a *parent contract*.

- Metaphor
    
    My grandpa has a recipe that tastes amazing. However, he’s getting old and I’m the young generation who prefers less salt. Here I would inherit from his recipe but `override` the adding salt process to make it more tasty for me.  
    
    ```solidity
    // Parent contract
    contract Recipe {
        function PutSomeSalt(uint amount) public virtual { }
    }
    
    // Child contract inheriting from Recipe
    contract MyRecipe is Recipe {
        function PutSomeSalt(uint amount) public override {
            // New implementation of PutSomeSalt function in the child contract
        }
    }
    ```
    
- Real Use Case
    
    In the ***[DemoToken](https://github.com/OpenZeppelin/defender-templates/blob/d101d4a9cd036b98e284d4169acf5959095523ab/defender/contract-wizard-deployer/contracts/DemoToken/DemoToken.sol#L28C4-L34C6)*** given by OpenZeppelin, the following code is given, which rewrites the ***_beforeTokenTransfer*** *function* in [ERC20](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/fd81a96f01cc42ef1c9a5399364968d0e07e9e90/contracts/token/ERC20/ERC20.sol#L348) to achieve the Pause function.
    
    ```solidity
    contract DemoToken is ERC20, ERC20Burnable, Pausable, Ownable, ERC20Permit, ERC20Votes {
    
        function _beforeTokenTransfer(address from, address to, uint256 amount)
            internal
            whenNotPaused
            override
        {
            super._beforeTokenTransfer(from, to, amount);
        }
        ...
    }
    ```
    

### Documentation

By using the `override` keyword in the *function* definition, you can *override* a *function* from the *parent contract*.

```solidity
//For example, here we define a ****foo function 
//and use override to override the foo function in the parent contract.
function foo() public override {
    
}
```

### FAQ

- How does Solidity know which function I’m overriding?
    
    By function name, parameter list, and return type. 
    
    *Overriding functions* must use the same **function name**, **parameter list**, and **return type** as the *function* being *overridden*. 
    
- Can constructors be overridden in Solidity?
    
    *Constructors* cannot be *overridden*; only additions are allowed based on the *parent contract's constructor*.
    

# Example/Example

```solidity
pragma solidity ^0.8.0;

contract Animal {
  //The "virtual" keyword will be discussed in the next section.
  function makeSound() public virtual returns (string memory) {
    return "Animal sound";
  }
}

contract Cat is Animal {
  //Override the parent's makeSound function.
  function makeSound() public override returns (string memory) {
    return "Meow";
  }
}

contract Dog is Animal {
  //Override the parent's makeSound function.
  function makeSound() public override returns (string memory) {
    return "Woof";
  }
}

contract AnimalSounds {
  Animal public animal;

  constructor(Animal _animal) {
    animal = _animal;
  }

  function makeAnimalSound() public returns (string memory) {
    return animal.makeSound();
  }
}
```
