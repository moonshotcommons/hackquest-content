# Content/概念

### Concept

在上一节中我们学习了函数的输入参数，而在函数处理完后，可能还需要输出一个信息，这就是函数的输出output。

- 比喻
    
    还是用我们黑匣子的例子，当黑匣子处理完信息后，他可能需要把处理完的结果返回给调用者。
    
- 真实用例
    
    就像ERC20的[***balanceOf***](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/8186c07a83c09046c6fbaa90a035ee47e4d7d785/contracts/token/ERC20/ERC20.sol#L106-L108)函数一样，输入一个地址来查询该地址的余额。而余额需要通过输出来返回给调用者。这样才完成了查询的整个步骤。
    
    ```solidity
    function balanceOf(address account) public view virtual returns (uint256) {
        return _balances[account];
    }
    ```
    

### Documentation

要定义*函数*的*输出*，我们添加一个 `returns`关键词。并且在函数体中使用`return`关键词返回函数输出。

```solidity
//此函数返回一个int型变量。
function sum(int a, int b) public returns(int) {
  return 1;
}
```

### FAQ

- 输出有什么用？
    
    函数输出可以用来判断函数被调用后的运行处理结果。
    
    例如，我们可以写一个判断年份是否为闰年的函数，输出一个bool值，我们通过*bool*值确定是否为闰年。
    
    ![844FA311-C825-459D-9041-919BEE8064C9.jpeg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5a8657b5-9a8c-474f-b4c7-4d039c4ec945/844FA311-C825-459D-9041-919BEE8064C9.jpeg)
    
- 什么是输出（返回值）？
    
    函数的*输出*是在*函数*执行完毕后返回给调用者的结果。
    
    ```solidity
    function name() public returns(int) {
        return 1;
    }
    ```

# Example/示例代码

```solidity
pragma solidity 0.8.4;

contract Function {
	//在这里定义名为add的公共函数，它接受两个int类型的参数a和b，并返回一个int类型的结果。
	function add(int a, int b) public returns(int) {
		return a + b;
	}
}
```
