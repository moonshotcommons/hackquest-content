# Content/Content

### Concept

So far, we have discussed the definition and initialization of structs. Next, we need to understand how to modify the properties within a struct.

After creating instances of the struct type, we often need to modify their property values. This may be necessary for updating data, recording new states, or performing other operations related to the struct.

- Metaphor
    
    Remember our discussion from the last lesson about the car manufacturing company and the blueprint analogy for struct initialization in Solidity? Let's build on that analogy to understand how to update a struct in Solidity.
    
    Recall that each car produced by your manufacturing company follows a blueprint that defines the model, price, color, and build year. When a customer buys a car, they receive a car with specific attributes based on this blueprint. This is analogous to initializing a struct in Solidity.
    
    Now, suppose a customer wants to modify the color of their car. They return to your manufacturing company, choose a new color from your catalog, and pay for the repainting service. Your team updates the car's color while keeping the rest of the attributes (model, price, build year) unchanged.
    
    ![Car_Struct_Update (1).png](Struct%20-%20Update%2057d9c7227ffb414b9439340c8b05ffe3/Car_Struct_Update_(1).png)
    
    In Solidity, updating a struct property is similar to the process of repainting a car. You can change a specific property of a struct instance while keeping the rest of the properties unchanged. However, the new value for the property must be of the same type as defined in the struct blueprint.
    
    So, updating a struct property in Solidity is like repainting a car in a different color. You're modifying one attribute, but the rest of the car (or struct) remains the same.
    
- Real Use Case
    
    Continuing from our previous discussion on the ***ERC20VotesLegacyMock*** *contract*, let's further explore how the ***[Checkpoint](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9e3f4d60c581010c4a3979480e07cc7752f124cc/contracts/mocks/token/ERC20VotesLegacyMock.sol#L15)*** struct is initialized and used.
    
    ```solidity
    struct Checkpoint {
        uint32 fromBlock;
        uint224 votes;
    }
    ```
    
    As a reminder, the ***[Checkpoint](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9e3f4d60c581010c4a3979480e07cc7752f124cc/contracts/mocks/token/ERC20VotesLegacyMock.sol#L15)*** struct records the block number (***fromBlock***) and the number of votes (***votes***) at that block. This allows the contract to track voting history.
    
    In the ***_writeCheckpoint*** *function*, the ***Checkpoint*** struct is initialized and populated.
    
    ```solidity
    function _writeCheckpoint(
            Checkpoint[] storage ckpts,
            function(uint256, uint256) view returns (uint256) op,
            uint256 delta
        ) private returns (uint256 oldWeight, uint256 newWeight) {
            uint256 pos = ckpts.length;
    				......
    				_unsafeAccess(ckpts, pos - 1).votes = SafeCast.toUint224(newWeight);
    				......
    }
    ```
    
    It updates the ***votes*** field of the last ***[checkpoint](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9e3f4d60c581010c4a3979480e07cc7752f124cc/contracts/mocks/token/ERC20VotesLegacyMock.sol#L15)*** with the new voting power value, ensuring that the voting power changes are recorded correctly.
    
    This continued use of struct update in the ***ERC20VotesLegacyMock*** *contract* demonstrates how structs can be employed to efficiently store and manage complex data in Solidity *smart contracts*. In this case, it provides a robust method to track the voting history for each account, allowing for greater transparency and traceability in the voting process.
    

### Documentation

To update a struct instance, you access the specific property of the struct instance and assign it a new value. Here's the syntax:

```solidity
StructName instance = StructName(value1, value2);
instance.property1 = newValue1;
```

### FAQ

- What requirement must be met when assigning a new value to a property in a Solidity struct instance?
    
    The new value to be assigned in a struct instance property must be of the same type as the property itself.
    

# Example/Example

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.4;

contract StructExample {

  struct Student{
    string name;
    uint studentId;
  }

  Student a = Student("Jane", 100);
  Student b = Student("Luca", 200);

  function updateStudentInfo() public {
    a.name = "john";
    b.studentId = 101;
  }
}
```
