# Content/Content

### Concept

In this lesson, we will learn about a string.

A *string* is used to represent textual data, like the name “GUA”, date “Dec 18, 2000”, or any text. 

- Metaphor
    
    Think of a *string* in Solidity like a notepad. Initially, this notepad can be empty or it might have some notes scribbled down. Just like you can write new notes, or erase, or edit the existing notes on the notepad, a *string* in Solidity is mutable, which means you can modify its content and length even after it has some initial text.
    
    Similarly, the *string* type in Solidity tells you it's a sequence of characters (like the notes on a notepad). These characters can represent names, descriptions, or any text data that the contract might need to handle.
    
- Real Use Case
    
    In the implementation of the ERC20 standard, the *string* data type is mainly used for the token's name and symbol. The name is usually the full name of the token, such as "Bitcoin Token" or "Ether Token". The symbol is the token's abbreviation, like "BTC" or "ETH". 
    
    These attributes are used to quickly identify the token when trading or viewing it. Below is the code that declares two strings ***[_name](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/token/ERC20/ERC20.sol#L45)*** and ***[_symbol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/token/ERC20/ERC20.sol#L46C4-L46C4)***. 
    
    ```solidity
    string private _name;
    string private _symbol;
    
    constructor(string memory name_, string memory symbol_) {
       _name = name_;
       _symbol = symbol_;
    }
    ```
    

### Documentation

To declare a *string* we use the keyword `string`, then express the textual content using either single or double quotes.

We can use `**=**` to assign the new value to it. 

```solidity
//here we define a string called myString
string myString = "I will be back!";
myString = 'No, you will not';
```

### FAQ

- Is the *string* type in Solidity a reference type?
    
    *string* is a reference type in Solidity and is mutable, meaning its length and content can be modified after initialization.
    
- When should we use a string?
    
    *Strings* are used for a variety of situations. Here are some examples:
    
    - Storing data: Strings can be used to store data that is required to be represented as text, such as names and addresses.
    - Messages: Strings can be used to create messages that are sent between smart contracts or between a smart contract and an external entity.
    - Error messages: When writing a function that requires certain inputs, you can use a *string* to create an error message that will be displayed if the input is not valid.
    
    ```solidity
    string data = "John Doe";
    string message = "Execution succeed";
    string error = "Error: invalid address";
    ```
    

# Example/Example

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.5.0;

contract LearningStrings {
  string car = "BMW";
  string text;
  //assign a value to a string variable using the function
  function setText () public returns (string memory) {
    text = "Hello World";
    return text;
  }
}
```
