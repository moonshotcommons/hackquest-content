# Content/Content

### Concept

Boolean otherwise known as bool is a type of variable whose value could only either be *true* or *false*.

- Metaphor
    
    Think of a boolean as a switch that can be either **on** or **off**. If the boolean is *true*, it's like the switch is on, and if it's *false*, it's like the switch is off.
    
- Real Use Case
    
    In the [ERC20](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/8186c07a83c09046c6fbaa90a035ee47e4d7d785/contracts/token/ERC20/ERC20.sol#L340-L351) approve authorization function, a *boolean variable* called ***emitEvent*** is required to indicate whether this authorization needs to trigger an *event*.
    
    ```solidity
    function _approve(address owner, address spender, uint256 value, bool emitEvent) internal virtual {
        ...
        if (emitEvent) {
            emit Approval(owner, spender, value);
        }
    }
    ```
    

### Documentation

```solidity
bool a = true;
bool b = false;
```

To define a boolean we use `bool`. 

### FAQ

- What are the operations on booleans?
    - **Negation**
        
        We have some operations on `bool`. Just like you could do plus and minus for numbers; for `bool`, we could do negation `!`  - which flips the value from *0* to *1* and from *1* to *0*.
        
        ```solidity
        bool c = !a; // c is false here, we flipped the value of a and assigned it to c
        bool d = !c; // d is true here  
        ```
        
    - **And**
        
        `&&` will return a value of *true* if both *variables* are *true*
        
        ```solidity
        bool e = d && a;// e will be true because both d and a are true 
        bool f = e && b;// f will not be true because b is not true
        bool g = e && true; // g will be true 
        ```
        
    - **Or**
        
        Since we have the `&&` operation, then we have or `||` too, which will return *true* if at least one of the two *variables* is *true*. 
        
        ```solidity
        bool h = true || false; // h is true
        ```
        
    - **Equality**
        
        Another operation that will be used commonly is `==` which will return *true* if two values are the same, *false* otherwise.
        
        ```solidity
        bool i = a == true; // i is true because a is true 
        ```
        
    - **Inequality**
        
        Finally, we also need inequality `!=`  which *returns* *true* if two values are not the same, *false* otherwise. 
        
        ```solidity
        bool j = a != true; // j is false because a is true
        ```
        

# Example/Example

```solidity
pragma solidity ^0.8.7;
contract Book{

	bool a = true;
	bool b = false;
	bool c = !a; 
	bool d = !c;
	bool e = d && a;
	bool f = e && b;
	bool g = e && true;
	bool h = true || false;
	bool i = a == true;
	bool j = a != true;
}
```
