# Content/Content

### Concept

An enum is a user-defined data type in Solidity. 

It's used to assign names to a set of *constants*, which makes a program easy to read and maintain.

- Metaphor
    
    An *enum* in Solidity is like a set of predefined labels that act as distinct choices on a menu, limiting your choices so there’s no confusion. It also makes ordering easier because you don’t need to know exactly what is in the food.
    
    Here in *enum* is the same. You could only assign predefined values to enum variables, and it’s human-friendly with labels. 
    
- Real Use Case
    
    In the [***GovernorCountingSimple***](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/governance/extensions/GovernorCountingSimple.sol#L15) contract developed by OpenZepplin, the ***VoteType*** enumeration is used to represent the type of vote: opposition, support and abstention.
    
    ```solidity
    enum VoteType {
        Against,
        For,
        Abstain
    }
    ```
    

### Documentation

To define an enum in Solidity, you use the `enum` keyword, followed by its name, and a list of members enclosed in `{}`.

```solidity
enum State { Waiting, Ready, Active }

```

### FAQ

- Why use enum?
    
    By using enums, you enhance the readability of your contract, reduce the chance of errors, and make your code more maintainable."
    

# Example/Example

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.17;

contract Example {
  enum City { NewYork, Tokyo, Shanghai }
}
```
