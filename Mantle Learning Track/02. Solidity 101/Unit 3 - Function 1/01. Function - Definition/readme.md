# Content/Content

### Concept

In Solidity, a function is a reusable piece of code that represents a specific action or computation within a *smart contract*.

<aside>
💡 It’s important to think of functions like black box when defining them:

- don’t know the detail
- don’t need to know the detail
- don’t want to know the detail

Only think about what you need to pass in for the function to work, and what output you want to get from the function. 

</aside>

- Metaphor
    
    You can consider a function as a black box for now. With given *inputs*,  it will do a set of predefined calculations and either output something or make some changes to your *variables*. 
    
    With functions, we could predefine some calculations and apply them to different *variables*. 
    
- Real Use Case
    
    In the ERC20 contract, we define a *function* called [***transfer***](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/8186c07a83c09046c6fbaa90a035ee47e4d7d785/contracts/token/ERC20/ERC20.sol#L118) whenever a user wants to send tokens, they will call this *function* without knowing what it does exactly but they know that their balance will decrease and the recipient’s balance will increase.
    
    ```solidity
    function transfer(address to, uint256 value) public virtual returns (bool) {
        ...  
    }
    ```
    

### Documentation

```solidity
//a function called sum
function sum() {
  //function body 
}
```

To define a function, we use the keyword `function` followed by its name. 

### FAQ

- What properties does a function have?
    
    Functions are defined with 
    
    1. a specific name 
    2. a list of parameters they take 
    3. [optionally] what they return. 
    4. different visibility specifiers like public, private, internal, or external, which dictate how the function can be called. 
    5. [optionally] view if they don't modify the state or pure if they neither read nor write the state. 
    6. [optionally] specific security modifiers
- What is a function header?
    
    As a black box, we need to define how it can be used, which means its name, inputs, and outputs. This is done by one line of code, we formally call it function header. 
    

# Example/Example

```solidity
pragma solidity ^0.8.4;
contract Function {
  //Here we define a function called add, which takes two int, a and b
  //and outputs another int.
  //public is indicating that everyone could access this function
  //we will discuss more about public in lesson Scope
  function add(int a, int b) public returns(int){
    return a + b;
  }
}
```
