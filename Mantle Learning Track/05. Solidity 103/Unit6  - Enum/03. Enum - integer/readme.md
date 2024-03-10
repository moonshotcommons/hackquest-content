# Content/Content

### Concept

In Solidity, *enum* types are stored by `uint8`. Each *enum* member is assigned an integer value, starting from *0* for the first member, *1* for the second, and so on. Therefore, an *enum* with *n* members will have integer values ranging from *0* to *n-1*.

In this unit, we will see how to use `min` / `max` in *uint8* to access the first and last element in the *enum*. 

- Metaphor
    
    Assigning integer values to enum members in Solidity is like giving each player in a team a jersey number, enabling quick identification and organization while maintaining a clear hierarchy of positions on the field.
    
- Real Use Case
    
    Still the same example, in the [***GovernorCountingSimple***](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/governance/extensions/GovernorCountingSimple.sol#L15) contract, if you want to get the maximum value of ***VoteType***, you can use the max syntax.
    
    ```solidity
    uint256 maxValue = VoteType.max;
    ```
    

### Documentation

We may use `type(EnumName).min/max` to get the first or last element in the enumerator. 

```solidity
type(Color).max;
type(Color).min;
```

### FAQ

- Can enums be cast to integers?
    
    Yes, *enums* in Solidity can be explicitly cast to their *integer* representation. This can be done using the `uint()` *function*. For example, if *state* is a variable of some *enum* type, *uint(state)* will give its integer value. However, it's worth noting that Solidity does not support implicit casting from *enum* to integer. You have to explicitly cast it.
    
    ```solidity
    Color red = Color.Red;
    uint r = uint(red);
    Color rred = Color(r);
    ```
    
- What does the `type` keyword return in Solidity?
    
    In Solidity, `type(SomeType)` returns a special object that provides meta-information about `SomeType`. For enums, it allows access to the minimum (`min`) and maximum (`max`) values of the enum. `type(EnumName).min` and `type(EnumName).max` return the first and last elements of the enum, respectively.
    
    ```solidity
    contract EnumDemo {
        enum Status {
            Pending,
            Shipped,
            Delivered,
            Canceled
        }
    
        function getMinStatus() public pure returns (Status) {
            return Status(type(Status).min);
        }
    
        function getMaxStatus() public pure returns (Status) {
            return Status(type(Status).max);
        }
    }
    ```
    

# Example/Example

```solidity
pragma solidity ^0.8.0;

contract EnumExample {
  enum ExampleEnum {
    Value1,
    Value2,
    Value3
  }

  function getMinMax() public pure returns (ExampleEnum, uint256) {
    uint256 minValue = uint256(type(ExampleEnum).min);
    uint256 maxValue = uint256(type(ExampleEnum).max);
    ExampleEnum e = ExampleEnum(minValue);
    return (e, maxValue);
  }
}
```
