# Content/概念

### Concept

在之前的章节中我们学习了不同的变量类型。接下来我们将会学习变量的两种定义方式：状态变量和局部变量。

- 比喻
    
    **合约**和**状态变量**的关系就像学校和学校的信息，该信息为学校内所有人员共享，维护的一个变量。并且其他人也可以随意的查询学校的信息。
    
- 真实用例
    
    在ERC20中，***[_totalSupply](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/8186c07a83c09046c6fbaa90a035ee47e4d7d785/contracts/token/ERC20/ERC20.sol#L43)***就是一个状态变量，它存储了该代币的总发行量。
    
    ```solidity
    uint256 private _totalSupply;
    ```
    

### Documentation

要定义一个 状态变量，我们需要将其放在函数之外。

```solidity
contract ContractName {
		//这是一个状态变量
    int a; 

		function add(int b) returns(int) {
			//b被定义为函数的输入参数，所以它不是状态变量
			//c是在函数中定义的，所以它也不是状态变量
			int c = a + b;	
			return c;
		}
}
```

### FAQ

- 什么是状态变量？
    
    状态变量是一种永久存在于区块链上的变量。
    
    例如，假设你有一个智能合约，用于跟踪网站上的按钮被点击的次数。你可以创建一个名为***clickCount***的状态变量，它从零开始，每次有人点击该按钮时，其值增加*1*。
    
    任何与合约交互的人都可以通过该状态变量来查询该按钮被点击了多少次。
    
- 何时使用状态变量？
    
    如果这个信息应该被记录在区块链上，则将其设置为状态变量。
    
    状态变量的通常需要更多的gas来读写，所以应当仅在必要时使用。
    
    ![Untitled](./img/1-1.png.png)
    
    <aside>
    💡 gas用于衡量执行智能合约操作所需的计算资源。
    
    </aside>

# Example/示例代码

```solidity
pragma solidity >=0.4.0 <0.9.0;

contract Book {
    int bookID;  //状态变量
    bool read;  //状态变量
    
    function a() public {
        bookID = 3;  //给状态变量赋值
        int bookId = bookID;  //bookId是在函数中定义的，不是状态变量
    }
}
```
