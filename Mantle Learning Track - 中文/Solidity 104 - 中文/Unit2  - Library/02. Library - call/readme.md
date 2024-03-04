# Content/概念

### Concept

在上一节中，我们学习了库（`library`）合约的定义，那么接下来，我们将学习如何使用`library`

- 比喻
    
    之前我们讲过调用函数就像按下黑盒子上的按钮，它将为你执行某些操作。库合约就像一个魔法盒子，里面充满了各种有用的功能。我们只需要使用库名+函数名的方式即可调用库合约中的函数。
    
    例如在上节课中我们定义了一个***MathLibrary***库，里面包含了一些数学运算，现在我们可以在另一个合约调用***square***函数计算一个数的平方：
    
    ```solidity
    MathLibrary.square(y);
    ```
    
    ![02AD2AAB-AAE1-459B-9A79-69A42BDC7937.jpeg](./img/2-1.jpeg)
    
- 真实用例
    
    在OpenZepplin的***[GovernorVotes](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/governance/extensions/GovernorVotes.sol#L25C1-L31C6)***合约中有一个获取时间的函数***clock***，在catch同调用了***[SafeCast](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/utils/math/SafeCast.sol#L475C1-L480C6)***的***toUint48***函数。
    
    ```solidity
    function clock() public view virtual override returns (uint48) {
        try token.clock() returns (uint48 timepoint) {
            return timepoint;
        } catch {
            return SafeCast.toUint48(block.number);
        }
    }
    ```
    

### Documentation

使用 `LibraryName.functionName()` 的方式调用库合约的函数。

```solidity
//调用MathLibrary库中的dosome函数
MathLibrary.dosome();
```

### FAQ

- library的call和contract call有区别吗
    
    有区别，比如我们在合约***A***中，尝试调用Library ***B*** 和 Contract ***C***。***B***实际算是***A***的一部分，所以***A***可以调用***B***中`internal`函数。
    
    而***C***不算，所以***A***不能调用***C***中的`internal`函数。

# Example/示例代码

```solidity
pragma solidity ^0.8.0;

library MathLibrary {
    function square(uint256 x) external pure returns (uint256) {
        return x * x;
    }
}

contract ExampleContract {
    function calculateSquare(uint256 y) external pure returns (uint256) {
        // 调用库合约的函数
        uint256 result = MathLibrary.square(y);
        return result;
    }
}
```