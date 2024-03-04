# Content/概念

### Concept

在本节中，我们将学习另一种类型，称为动态数组。

数组是一种用来存储相同类型数据的集合。

- 比喻
    
    例如一个班级里的学生集合，我们可以将每个学生看作是集合中的一个元素，而班级则是一个数组。
    
- 真实用例
    
    在OpenZepplin的***GovernorStorage***合约中，定义了一个*uint256*的数组***[_proposalIds](https://github.com/OpenZeppelin/openzeppelin-contracts-upgradeable/blob/7d7ad99dee371e0ee042e2999aaf43941dea1513/contracts/governance/extensions/GovernorStorageUpgradeable.sol#L24)***，用来存储已经提交提案的***proposald***。
    
    ```solidity
    uint256[] private _proposalIds;
    ```
    

### Documentation

为了定义动态数组，你需要使用`类型`+`[]`的方式定义。

```solidity
uint256[] arr;
```

在这里我们定义了一个名为***arr***的*uint256*类型的动态数组。

### FAQ

- 动态数组和静态数组有什么区别？
    
    静态数组需要在声明时确定的固定大小，而动态数组的大小可以在运行时进行调整。
    
    例如，我们需要将1，2，3这三个数字存入数组中，使用固定大小为5的静态数组和使用动态数组的内存占用情况如图：
    
    ![31778B19-9FC7-417C-8270-D9C9242BD947.jpeg](./img/1-1.jpeg)
    
- 动态数组有什么优点？
    1. 可以在运行时根据需要调整大小。
    2. 只占用实际元素所需内存空间，节省内存。
    3. 可以使用多种函数和操作进行元素操作，更加灵活易用。

# Example/示例代码

```solidity
pragma solidity ^0.8.0;

contract Example {
  //这里我们定义了一个名为nums的uint256类型的动态数组
  uint256[] nums;
}
```
