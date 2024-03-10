# Content/Content

### Concept

In Solidity, *variables* are used to store and manage data within *smart contracts.*

At the same time, we will also learn `int` for representing integers.

- Metaphor ****
    
    *Variables* are like containers that store information within a program (a smart contract here). 
    
    Imagine a container that you put things into, like a box or a jar. In the case of Solidity, the container is a variable, and it can hold different types of data such as *numbers*, *text*, or *addresses*. 
    
- Real Use Case
    
    The [***average](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/8186c07a83c09046c6fbaa90a035ee47e4d7d785/contracts/utils/math/SignedMath.sol#L28-L32)*** function in the OpenZeppelin ***SignedMath*** *contract* uses `int256` to represent the *parameters* involved in the calculation, which means that this *function* can perform calculations with both positive and negative numbers.
    
    ```solidity
    function [average](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/8186c07a83c09046c6fbaa90a035ee47e4d7d785/contracts/utils/math/SignedMath.sol#L28-L32)(int256 a, int256 b) internal pure returns (int256) {
        // Formula from the book "Hacker's Delight"
        int256 x = (a & b) + ((a ^ b) >> 1);
        return x + (int256(uint256(x) >> 255) & (a ^ b));
    }
    ```
    

### Documentation

*Variables* are declared with their type, followed by the variable name.

```solidity
int basic_price;
```

### FAQ

- How to assign value to a variable?
    
    ```solidity
    int basic_price = 3;
    ```
    
    We assign values using `=` followed by its value. 
    
- What properties does a variable have?
    
    Every *variable* has a type, as a shoe container could only hold shoes, you cannot assign a *true* or *false* value to an `int` type *variable*, which should hold *integers*. 
    
    Overall, a *variable* also has：
    
    - Variable name: this is the name we give to a container: ***a***
    - Variable value: is the actual information we put inside the container: *10*
    - Variable type: every *variable* has a type, for example: `integer`

# Example/Example

```solidity
pragma solidity ^0.8.7;
contract Book {

  //This is a variable of type integer 
  int basic_price = 10;

}
```