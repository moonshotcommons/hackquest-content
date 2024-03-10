# Content/Content

### Concept

Up until now, we have covered various *variable types*, including booleans, integers (signed and unsigned), address, and mapping. In this section, we will introduce another data type: structs.

Structs in Solidity let you define custom data types by grouping multiple *variables* of different types.

- Metaphor
    
    Think of a struct like a student's report card. In a report card, there are several pieces of information like the student's name, student ID, and grades for various subjects. All this information is related to the same student, so it's bundled together in one report card.
    
    Similarly, a struct in Solidity allows you to create a custom data type with multiple properties. In the case of ***Student***, a *struct* can bundle together data like the student's name, student ID, and grade in one unit.
    
    ```solidity
    struct Student {
      string name;
      uint256 studentId;
      uint256 grade;
    }
    ```
    
- Real Use Case
    
    The ***ERC20VotesLegacyMock*** contract is an extension of the ERC20 standard that adds functionality for token-based voting. This contract uses the ***[Checkpoint](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9e3f4d60c581010c4a3979480e07cc7752f124cc/contracts/mocks/token/ERC20VotesLegacyMock.sol#L15)*** struct to track the voting power of token holders over time.
    
    The ***[Checkpoint](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9e3f4d60c581010c4a3979480e07cc7752f124cc/contracts/mocks/token/ERC20VotesLegacyMock.sol#L15)*** struct is defined with two fields, ***fromBlock*** and ***votes***, that respectively record the block number and voting power at the time of a specific change in a holder's balance.
    
    ```solidity
    struct Checkpoint {
        uint32 fromBlock;
        uint224 votes;
    }
    ```
    
    Whenever a user's voting power changes, a new ***[Checkpoint](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9e3f4d60c581010c4a3979480e07cc7752f124cc/contracts/mocks/token/ERC20VotesLegacyMock.sol#L15)*** is created. This provides a historical record of voting power, essential for governance systems that rely on token-based voting.
    

### Documentation

```solidity
struct Cat {
  string name;
  address owner;
  uint256 age;
}
```

To define a struct, use the `struct` keyword followed by the name of the struct. 

Then enclose its properties in curly braces, separating each with a semicolon. 

### FAQ

- Why Use Structs?
    
    Struct declarations are similar to class declarations in **Java**. They provide an easy way to organize and manage related data, making your code clearer and comprehensible.
    

# Example/Example

```solidity
pragma solidity ^0.8.0;

contract Example {
  //Here is a struct definition for a Student with three properties:
  //name，studentId，grade
  struct Student {
    string name;
    uint256 studentId;
    uint256 grade;
  }
}
```
