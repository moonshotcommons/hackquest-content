# Content/概念

### Concept

在上一节中，我们学习了如何定义 contract（合约），而我们本节要学习的内容是合约中最关键的基石——variable（变量）。

同时我们将学习一个最基础的变量类型 - int。

> 这是一个表示整数的变量类型。
> 
- 比喻
    
    *变量* 就像程序（在这里指智能*合约*）内部存储信息的**容器**。
    
    想象一下一个可以放东西的容器，比如一个盒子。在 Solidity 中，这个**容器**就是一个*变量*，它可以存储不同类型的数据，例如数字、文本或地址。
    
    每个*变量*都有一个类型，就像鞋盒只能放鞋子一样，在 int 类型的*变量*中你不能分配 *true* 或 *false* 值，因为它应该只能存储**整数**。
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/557996cc-ca19-47fd-ad11-d26707fde1f2/Untitled.png)
    
- 真实示例
    
    在OpenZepplin的SignedMath合约中的[***average()***](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/8186c07a83c09046c6fbaa90a035ee47e4d7d785/contracts/utils/math/SignedMath.sol#L28-L32)函数使用`int256`来表示参与运算的参数，也就意味着该函数可以进行正/负数的计算。
    
    ```solidity
    function [average](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/8186c07a83c09046c6fbaa90a035ee47e4d7d785/contracts/utils/math/SignedMath.sol#L28-L32)(int256 a, int256 b) internal pure returns (int256) {
        // Formula from the book "Hacker's Delight"
        int256 x = (a & b) + ((a ^ b) >> 1);
        return x + (int256(uint256(x) >> 255) & (a ^ b));
    }
    ```
    

### Documentation

我们可以通过以下的方式为变量赋值

```solidity
//定义一个整形变量a
int a;

a = 10;//a为10
a = a + 10; // a现在为20
```

### FAQ

- 变量由什么构成？
    
    一个*变量*由三部分组成：
    
    - *变量*名称：这是我们给容器取的名字
    - *变量*类型：每个*变量*都有一个类型，例如*整数*
    - *变量*值：实际放入容器中的信息
    
    例如在下面例子中，*变量*名称为 ***a*** ，*变量*类型为 int ,变量值为*100*。
    
    ```solidity
    int a = 100;
    ```
# Example/示例代码

```solidity
pragma solidity ^0.8.7;
contract Book {

  //这是一个类型为int的变量，并将其初始化为10
  int basic_price = 10;

}
```