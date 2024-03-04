# Content/概念

### Concept

在这一节中，我们将学习库的一种特殊用法——将库合约中的函数附加到任何类型中。

实际上就是给一个普通的类型增加了一些库合约中的函数的功能，让它变得更加强大和有趣。

指令`using A for B;`可用于将库 ***A***的所有函数附加到到任何类型B。添加完指令后，库 ***A***中的函数会自动添加为B类型变量的成员，可以直接使用`B.functionName()`调用。

- 比喻
    
    就好像是在把一个魔法标签贴在类型B上，标签上写着“A”。一旦贴上了这个标签，类型B就会变得神奇起来，因为它会自动拥有库***A***中的所有函数。
    
- 真实用例
    
    在Uniswap v3的***[UniswapV3Pool](https://github.com/Uniswap/v3-core/blob/d8b1c635c275d2a9450bd6a78f3fa2484fef73eb/contracts/UniswapV3Pool.sol#L33C1-L34C31)***合约中也使用到了刚刚提到的库。
    
    ```solidity
    using SafeCast for uint256;
    using SafeCast for int256;
    ```
    

### Documentation

使用`using...for...`语句可以将库中的函数附加到某个类型中。

```solidity
//将MathLibrary库附加到uint256类型上
//这样所有的uint256类型的变量都可以直接使用MathLibrary库中的函数
using MathLibrary for uint256;
```

### FAQ

- 通过variableName.functionName()调用和通过直接调用库函数functionName()有什么区别？
    
    如果库函数有参数的话，`变量a.functionName()`的方式会自动把变量作为函数的第一个参数传入。
    
    <aside>
    💡 详见example
    
    </aside>
    

# Example/示例代码

```solidity
pragma solidity ^0.8.0;

library MathLibrary {
    function square(uint256 x) external pure returns (uint256) {
        return x * x;
    }
}

contract ExampleContract {
    using MathLibrary for uint256;
    
    function calculateSquare(uint256 y) external pure returns (uint256) {
        // 调用库合约的函数，y变量将默认作为第一个参数传入square函数。
        return y.square();
    }
}
```