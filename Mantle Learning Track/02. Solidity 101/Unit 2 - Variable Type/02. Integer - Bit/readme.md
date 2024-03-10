# Content/Content

### Concept

A bit is a unit. It represents a single digit in binary representation: 0 or 1. And `uint` can specify how many bits it stores, like this: `uint128`.

- Metaphor
    
    Imagine you're constructing a language from scratch. You have a set of basic building blocks, like letters of the alphabet, that you can use to create words. Each letter is a bit.
    
- Real Use Case
    
    In [UniswapV2](https://github.com/Uniswap/v2-core/blob/ee547b17853e71ed4e0101ccfd52e70d5acded58/contracts/libraries/UQ112x112.sol#L9), developers split `uint224` into **uint112 x uint112** to achieve decimal representation in Solidity. The first 112 **bits** are used to represent the integer part, while the subsequent 112 **bits** are used for the decimal part.
    
    ```solidity
    uint224 constant Q112 = 2**112;
    ```
    

### Documentation

```solidity
uint8 a;
int256 b;
int128 c;
uint127 d; //This is NOT valid because 127 is not a multiplier of 8.
```

You can’t use bit in Solidity directly, as it’s used to specify the number of bits an integer could use. 

We add bits after `uint` or `int`.

However, it’s worth noting that the number of bits needs to be a multiplier of 8.

### FAQ

- What is **one bit**?
    
    One bit is one digit of a binary number, so either a *1* or a *0*. 2 bits means two digits: *00*,*01*,*10*,*11* so 4 numbers could be represented. 
    
- What does it mean by “**unsigned integer of size 256 bits**”?
    
    256 bits means there could be 256 bits to be used to store the value. If every bit is a *0* or *1*, how many different representations these 256 *bits* could have? 2 to the power of 256, which is approximately 10^77, which says any number smaller than 10^77 could be assigned to a variable of type uint256. 
    
- Why do we **specify** the number of bits needed for this integer?
    
    This is because larger numbers require more storage space, which increases costs. Therefore, we’d like to know how big our integers could be and then use no more than that.
    
- uint and int
    
    uint and int are the acronym of uint256 and int256, which are the biggest integers we could have. 
    
    ```solidity
    uint a;//this is the same as uint256 a;
    int b;
    ```
    

# Example/Example

```solidity
pragma solidity ^0.8.4;

contract Book {
  int bookID; // unsigned int 
  int16 price; // signed int
}
```