# Content/概念

### Concept

变量可以分为 *状态变量* 和 *局部变量*， *函数*也可以分为3种 —— pure函数、view函数和其他函数。

在这一章中，我们首先学习纯函数-pure，所谓纯函数就是该函数不会访问以及修改任何状态变量。

<aside>
💡 一般来讲pure函数用于返回一个固定的值或完成计算。

</aside>

- 比喻
    
    pure函数就像是计算器，你只是输入数字和运算符，并等待计算器返回结果。
    
    并且该计算器能获取的信息只有你的输入，它并不能从其他地方获取信息，也不会对任何事物造成影响。
    
- 真实用例
    
    在Openzepplin的***governance***合约有一个***[votingDelay](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/mocks/governance/GovernorVoteMock.sol#L13)***的函数，用于返回当前投票的延迟。
    
    ```solidity
    function votingDelay() public pure override returns (uint256) {
        return 4;
    }
    ```
    

### Documentation

要将一个*函数*定义为 pure函数，我们需要在*函数头*中使用关键字 `pure`。

```solidity
function add() public pure {
	//function body 
}
```

<aside>
💡 为了保持一致性，我们建议遵循此顺序：函数名称 、参数、作用域、状态可变性、返回值。

</aside>

### FAQ

- 为什么要使用pure定义函数？
    
    使用pure定义的函数被调用时不用花费gas，并且可以保证该函数不会改变状态变量，有益于开发时的模块化管理。

# Example/示例代码

```solidity
pragma solidity ^0.8.0;

contract Example {
    mapping(int => int) aa;
		//这是一个pure函数
    function add(int a, int b) public pure returns(int) {
        return a + b;
   }
		//这不是一个pure函数
   function addNotPure(int a, int b) public returns(int) {
       aa[0] = a + b;
       return aa[0];
   }
}
```

# **Button/Try it out**