# Content/Content

### Concept

In the previous content, we have already learned a signed integer representation called int, and now we are going to learn about an **unsigned integer variable** called uint.

`int` **could be both positive and negative, while `uint` could only be positive. 

```solidity
//int could be negative, like -3
int a = -3;

//uint could only be positive
uint b = 10; // this is ok
uint c = 3 - 5; // this will report errors
```

- Real Use Case
    
    In the [ERC20](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/8186c07a83c09046c6fbaa90a035ee47e4d7d785/contracts/token/ERC20/ERC20.sol#L43) contract, we use an `uint256` variable to **track** the total supply of tokens.
    
    ```solidity
    uint256 private _totalSupply;
    ```
    

### Documentation

To define and assign an integer

```solidity
int ourInteger = -10;
uint outUInt = 10;
```

### FAQ

- Why do we use unsigned integers?
    
    Well, this is because if we want to store the same positive number, uint could need smaller memory as it doesn’t need to store the symbol. Since we don’t need to store the symbol of the integer (**`-`** or **`+`**) then we could have more space to store the actual number. 
    
- What are the common operations of integers?
    
    **+= and -=**
    
    Two commonly used operations for updating an integer are `+=` and `-=` 
    
    `a += b` is the same as `a = a + b` ****we retrieve the value of ***a***, add ***b*** to it, and assign the value back to ***a***. 
    
    ```solidity
    int a = 3;
    //this is the same as a = a + 3
    //We retrieve the value of a
    //add 3 to it
    //and assign it back to a 
    a += 3; //a is 6 now 
    ```
    
- Anything else?
    
    **Comparison**
    
    We could also compare two numbers and return a bool.
    
    ```solidity
    bool d = 10 > 3; // d will be true because 10>3 
    bool e = 3 <= 3; // e will also be true, <= means less than or equal to
    ```
    
    **Equality and Inequality**
    
    Also, **equality** and **inequality** work for *integers*.
    
    ```solidity
    bool f = a == 10;// f is false because a is not 10 as we defined in += and -= section 
    bool g = a != 10;//g is true 
    ```
    

# Example/Example

```solidity
pragma solidity ^0.8.4;

contract Book {
    uint bookID; // unsigned int 
		int price; // signed int
}
```