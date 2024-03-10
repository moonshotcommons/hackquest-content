# Content/Content

### Concept

In Solidity, a contract is a collection of code (*functions*) and data (*state*) that resides at a specific address on the Ethereum blockchain. 

A *contract* in Solidity is like a class in Java.

- Metaphor
    
    A contract is like an automatically executing agreement, but it is not enforced by legal institutions; instead, it is executed by computer nodes on the blockchain network.
    
- Real Use Case
    
    Every ERC20 *token* (like the stablecoin DAI) is regulated by a *contract*, consisting of a collection of code (how to **transfer**, **check balance**, **mint new tokens**) and data (balance of each *address*). 
    

### Documentation

```solidity
//Here we defined a contract called Name
contract Name{ }
```

To define a *contract*, we use the keyword `contract` followed by the name of the *contract*.

### FAQ

- What are similar features in other languages that are comparable to contracts?
    
    *Contracts* in Solidity are similar to **classes** in **object-oriented languages**, with each *contract* containing declarations of *state variables*, *functions*, and more.
    
    In Solidity, a .sol file, which is the extension for Solidity source code files, could contain one or more *contracts*. 
    

# Example/Example

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.18;
//the contract named "Book"
contract Book{

  //this is an empty contract
	
}
```