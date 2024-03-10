# Content/Content

### Concept

In the last section, we learned about what is enum. Now, let’s see how to assign a value to an enum type variable.  

- Metaphor
    
    Assigning a value to an enum in Solidity is like giving a unique identity badge to different members of a club, making it easy to recognize and categorize them based on their roles without the need for lengthy introductions.
    
- Real Use Case
    
    In the ***[IGovernor](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/governance/IGovernor.sol#L13)*** contract, the following code assigns value to the enum ***ProposalState*** to represent the different states of the proposal. 
    
    ```solidity
    enum ProposalState {
            Pending,
            Active,
            Canceled,
            Defeated,
            Succeeded,
            Queued,
            Expired,
            Executed
        }
    ```
    

### Documentation

To assign a value to an *enum*, you reference the name followed by the dot **`.`** operator, and then the desired value.

```solidity
enum State { Waiting, Ready, Active }
State s = State.Active;
```

### FAQ

- Is the enum variable reference type or value type?
    
    An enum variable is a value type because its value is stored in `uint8`, which is a value type. 
    
- Could we assign **integer values** to enum variables?
    
    You can do explicit conversion between enum and integer, but you cannot do implicit conversion. 
    
    ```solidity
    Season public season = 1;  // implicit conversion, this will be error
    Season public season = Season(1);  // explicit conver, this will work
    ```
    

# Example/Example

```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.17;

contract Example {
  enum City { NewYork, Tokyo, Shanghai }
  City public favoriteCity;

  function setFavoriteCityToTokyo() public {
    favoriteCity = City.NewYork;
  }
}
```
