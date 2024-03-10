# Content/Content

### Concept

In previous lessons, we extensively covered Solidity inheritance. Now, let's explore **multiple inheritance**.

Multiple inheritance allows a *contract* to inherit features and attributes from multiple *parent contracts*. It's like combining puzzle pieces to create a more complex puzzle. 

- Metaphor
    
    Imagine that you are writing your own personal cookbook. There are two cookbooks on the market to choose from: one is a Sichuan recipe, and the other is a Cantonese recipe. Now you want to include Sichuan and Cantonese cooking techniques in your recipes.
    
    To achieve this, you can create a new cookbook that *inherits* the Sichuan and Cantonese recipes. Through this method of multiple inheritance, your recipes will have the cooking skills of Sichuan and Cantonese cuisine.
    
- Real Use Case
    
    For example, we want to create custom tokens with ERC20 *standard* features and ownership management. We can use **multiple inheritance** to inherit both the ERC20 *contract* and the ***Ownable** contract*.
    
    ```solidity
    contract MyToken is ERC20, Ownable { }
    ```
    

### Documentation

To *inherit* from multiple *contracts*, we separate the *contract* with a comma. 

```solidity
//Use is keyword for multiple inheritance, followed by a comma-separated list of contracts.
contract Child is Parent1, Parent2 {

}
```

### FAQ

- Why multiple inheritance is needed?
    
     In order to facilitate contract management, when the project complexity is high, multiple inheritance can be used to make the code structure clearer, and also make the code modular and easy to maintain.
    

# Example/Example

```solidity
pragma solidity ^0.8.0;

contract Parent1 {
  function foo() public virtual returns (string memory) {
    return "Parent1";
  }
}

contract Parent2 {
  function foo() public virtual returns (string memory) {
    return "Parent2";
  }
}

contract Child is Parent1, Parent2 {
  //it will return Parent2。
  function foo() public override(Parent1, Parent2) returns (string memory) {
    return super.foo();
  }
}
```
