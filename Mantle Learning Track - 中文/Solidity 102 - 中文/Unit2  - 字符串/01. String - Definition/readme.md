# Content/概念

### Concept

在本课程中，我们将学习一个新的变量类型：字符串类型string。

字符串是一种表示文本数据的数据类型。字符串是由一系列字符组成，例如数字、字母、标点符号等。

- 比喻
    
    你可以将字符串想象成一段话、一首歌曲的歌词、一篇文章或者任何包含文字的东西。
    
    ![FE5260B5-9C3C-4B90-8C5C-D3F31B9B46D7.jpeg](./img/1-1.jpeg)
    
- 真实用例
    
    在ERC20标准的实现中，*string*数据类型主要用于代币的名称和符号。 名称通常是代币的全名，例如“比特币代币”或“以太币代币”。 符号是代币的缩写，如“BTC”或“ETH”。
    
    这些属性用于在交易或查看代币时快速识别该代币。 下面是声明两个字符串***[_name](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/token/ERC20/ERC20.sol#L45)*** 和 ***[_symbol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/token/ERC20/ERC20.sol#L46C4-L46C4)***的代码：
    
    ```solidity
    string private _name;
    string private _symbol;
    
    constructor(string memory name_, string memory symbol_) {
       _name = name_;
       _symbol = symbol_;
    }
    ```
    

### Documentation

在Solidity中声明字符串非常简单。要声明一个字符串，我们使用关键字`string`：

```solidity
string myString = "I will be back!";

//String作为参数时必须指定其存储的位置，在大多数场景中都使用memory
constructor(string memory name_, string memory symbol_) {
    _name = name_;
    _symbol = symbol_;
}
```

### FAQ

- 字符串有什么用？
    
    可以使用字符串来存储需要表示为文本数据，例如名称和地址。
    
    字符串还用于创建消息和错误消息。
    
    例如，我们之前学习的`require`语句，我们将字符串作为第二个参数传递给 require 函数，以便在发生异常时向用户显示错误消息。
    
    ```solidity
    require(a > 5, "Value must be greater than 5");
    ```
    

# Example/示例代码

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.4;

contract LearningStrings {
    string car = "BMW";
    string text;
    //使用函数将值赋给字符串变量
    function setText () public returns (string memory) {
        text = "Hello World";
        return text;
    }
}
```

