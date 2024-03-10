# Content/Content

### Concept

Every Solidity file has one line of code that looks like this.

```solidity
pragma solidity ^0.8.4;
```

Here we use the keywords `pragma solidity` to specify the version of the Solidity compiler to be used to compile the code. 

<aside>
💡 pragma doesn’t change the *compiler* version, it just requires the *compiler* to check if the version matches.

</aside>

- Metaphor
    
    Compiler is a special type of program, and you can think of it as a translator, that translates something you write (code in Solidity) (the “source language”) to something that a computer could understand (0 and 1s). 
    
    Pragma is like defining a translator’s version.
    
- Real Use Case
    
    In the latest version of **[*ERC20*](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/8186c07a83c09046c6fbaa90a035ee47e4d7d785/contracts/token/ERC20/ERC20.sol#L4)**, a compiler version of no less than 0.8.20 is used.
    
    ```solidity
    pragma solidity ^0.8.20;
    
    abstract contract ERC20 is Context, IERC20, IERC20Metadata, IERC20Errors { }
    ```
    
    This way, only **compilers** with a version greater than or equal to *0.8.20* but less than *0.9.0* can compile this ***ERC20*** contract. This helps to avoid potential compatibility issues between the code and compiler versions
    

### Documentation

We use  *^0.a.b* to indicate code in the current file needs solidity **≥***0.a.b* and *<0.(a+1).0.*

```solidity
//Here it says we need version >=0.7.5, but <0.8.0
pragma solidity ^0.7.5;
```

### FAQ

- What is a compiler?
    
    A *compiler* in the context of Solidity is a software tool that translates human-readable Solidity source code into machine-readable bytecode, which can be executed on the Ethereum Virtual Machine (EVM).
    
- What if we need an exact version to compile?
    
    We could use
    
    ```solidity
    pragma solidity 0.8.4;
    ```
    
    to indicate that we need exactly version *0.8.4* to compile our code.
    
- Why do we have different versions?
    
    Solidity is constantly evolving as a programming language with new features and bug fixes. 
    
    For example, some syntax may not be available in earlier versions or later versions; or some keywords are required in the earlier versions, but not later versions. 
    
    When you write a Solidity *smart contract*, you want to ensure that it is compiled using the right version. Otherwise, the program may not be able to compile.  
    

# Example/Example

```solidity
pragma solidity ^0.4.3;
```
