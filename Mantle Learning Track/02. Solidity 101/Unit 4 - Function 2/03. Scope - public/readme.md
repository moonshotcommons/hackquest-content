# Content/Content

### Concept

When defining variables and functions, we also need to define visibility, also called scope. It says when we can access this *variable* or *function*. 

**Public**

As the name suggests, any *variables* and *functions* that are marked to be public could be accessed from anywhere, by functions both in this *contract* and other *contracts*. 

- Metaphor
    
    Think of a contract like a household. For all the people in the world, they either live in your household or not. All the *functions* and *variables*, either exist in the same contract or not. 
    
    `public` means anyone, both in and out of the household could access the content.  
    
- Real Use Case
    
    ```solidity
    function name() public view virtual returns (string memory) {
        return _name;
    }
    ```
    
    In the ERC20 contract, the ***[name](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/8186c07a83c09046c6fbaa90a035ee47e4d7d785/contracts/token/ERC20/ERC20.sol#L67C5-L69C6)*** function is marked as `public`. It is readable **directly** from external contracts or interfaces without the need for getter functions.
    

### Documentation

To define a *public variable* or a *public function*, we use the keyword `public`, and we put it before the name of the *variable* or after the parameter of a *function*.  

```solidity
uint public a;
function aa() public { 
  //funciton body 
}
```

### FAQ

- Isn’t everything in Ehtereum blockchain public?
    
    It’s public to users (nodes), but not other smart contracts. All the contract or transactions are public to all nodes because we need the network to confirm transactions, but to smart contracts we could still have some access control.
    

# Example/Example

```solidity
pragma solidity ^0.8.4;
//If we put the code in Remix and deploy it
//we could see that we could access the function aa
//and also the variable a, because they’re public. 
contract A {
  uint public a;
  function aa() public {
    //this is the same as a = a+1 ;
    a++;
  }
}
```
