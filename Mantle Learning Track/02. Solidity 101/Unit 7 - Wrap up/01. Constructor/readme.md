# Content/Content

### Concept

The constructor in Solidity is a special function executed **only once** during the deployment of a *smart contract* to **initialize** its *state variables* and perform setup tasks.

If you don’t define a constructor, an empty *constructor that* does nothing will be created by Solidity when deploying the *contract*. 

- Metaphor
    
    The *constructor* in Solidity is like the grand opening ceremony of a new building, where all the essential arrangements and setup are done before the building is officially open to the public.
    
- Real Use Case
    
    ```solidity
    constructor(string memory name_, string memory symbol_) {
        _name = name_;
        _symbol = symbol_;
    }
    ```
    
    A real use case of a [constructor](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/token/ERC20/ERC20.sol#L59-L62) in an ERC20 token contract is to set initial values for the token's properties, such as *name*, and *symbol*. 
    
    Every ERC20 has a name and symbol, to maintain clarity and prevent confusion, it's advisable to choose unique and distinctive name and symbol values for each token. 
    
    The *name* parameter represents the full name or title of the token. It provides a human-readable description that helps users and developers easily identify and understand the purpose of the token. This can be particularly useful when displaying the token's name in user interfaces, wallets, exchanges, and other platforms. The *name* parameter is essentially a more descriptive label for the token.
    
    The *symbol* parameter is a shorthand representation of the token's name. It typically consists of a few characters and is often used as a ticker symbol to identify the token in a concise manner. This is especially important in scenarios where space is limited, such as in trading interfaces or when displaying a list of tokens. The *symbol* parameter is designed to provide a quick and recognizable identifier for the token.
    

### Documentation

```solidity
constructor(int a, bool b) {
  //function body
}
```

To define a constructor, we use the keyword `constructor`, followed by *parameters* and that’s it.

### FAQ

- What is the difference between a constructor and a function?
    
    Constructors don’t have 
    
    1. **name** - you don’t need a name because there is only one **constructor** and it will be called automatically
    2. **returns** - there’s no return because the **constructor** is for setting up 
- Why do we need a constructor?
    
    There are two reasons.
    
    1. Avoid extra setup steps. There’s some information we want to setup at the time of *contract* deployment. We use a *constructor* to **avoid an extra setup step after deployment**. 
    2. Access control. For example, we want to issue our own tokens, and I want to define that only I could mint tokens. How do I inform the *contract* of this piece of information? We set this up at the deployment time —— who **deploys** the *contract*, who is the **owner**.  
    

# Example/Example

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;

contract A {
    uint public a;

    constructor(uint a_) {
        a = a_;
    }
}

contract B {
		//an empty constructor
    constructor() {}
}
```
