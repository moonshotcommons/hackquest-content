# Content/概念

### Concept

在这一节中，我们将会学习一个新的数据类型——Enum，也称为*枚举*。

在 Solidity 中，"enum"（枚举）是一种用户定义的数据类型，用于创建一组命名的常量。枚举通常用于为合约状态或其他固定值集合定义清晰和易读的名称。

- 比喻
    
    例如，当人们计划旅行时，季节是一个重要的考虑因素。使用Enum来表示季节，可以让旅行者了解目的地的气候和天气条件，从而决定最佳的旅行时间。
    
    一年中有春夏秋冬四种季节，我们可以创建一个枚举类型来表示季节的选项：
    
    ```solidity
    enum Season {
      Spring,
      Summer,
      Autumn,
      Winter
    }
    ```
    
    在上述示例中，我们定义了一个名为***Season***的枚举类型，其中包含了四个选项：*Spring*，*Summer*，*Autumn*和*Winter*。
    
    ![B562174A-FF3E-48A3-ADB3-F5572BB0C191.jpeg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2eb984a6-2c14-48b0-96e7-b65fbb27c37c/B562174A-FF3E-48A3-ADB3-F5572BB0C191.jpeg)
    
- 真实用例
    
    在OpenZepplin开发的[***GovernorCountingSimple***](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/governance/extensions/GovernorCountingSimple.sol#L15)合约中，使用了***VoteType***枚举，用于表示投票的类型：反对，支持和弃权。
    
    ```solidity
    enum VoteType {
        Against,
        For,
        Abstain
    }
    ```
    

### Documentation

在定义枚举类型时，需要使用`**enum**`关键字，其后是枚举的名字，随后用`{}`将枚举变量括起来，每个枚举值之间用`,`分隔。

例如在这里我们定义了一个名为***City***的枚举类型，其中有*Beijing*，*HangZhou*，*ChengDu*三个枚举值。

```solidity
enum City {
  BeiJing,
  HangZhou,
  ChengDu
}
```

### FAQ

- 为什么使用枚举？
    
    枚举类型的使用可以带来以下好处：
    
    1. **可读性：** 枚举为取值提供了有意义的名称，使得代码更易读、理解。
    2. **可维护性：** 枚举定义了取值的固定范围，使得代码更易于维护和修改。
    3. **类型安全：** 枚举类型限制了变量的取值范围，避免了无效或不一致的取值，提高了代码的安全性和可靠性。

# Example/示例代码

```solidity
pragma solidity ^0.8.0;

contract Example {
  //定义了一个枚举类型City
  enum City {
    BeiJing,
    HangZhou,
    ChengDu
  }
}
```
