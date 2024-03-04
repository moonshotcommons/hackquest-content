# Content/定义balanceOf函数

刚刚我们提到这个函数是用来查询余额的，所以我们需要一个入参来表示要查询的账户地址。

查询函数不应该修改合约的状态变量，因此该函数应该带有`view`修饰符。

在选择函数的可见性时，我们选择使用`public`，这样无论是在合约内部还是在合约外部，都可以访问该函数以查询余额。

由于是查询余额，因此在函数的返回值部分，我们需要返回余额。在前一节中提到，余额一定是非负的，因此我们选择使用`uint256`作为返回值类型。

**Syntax**

view return scope function

- 提示
```solidity
//例如在这里，我们定义了一个函数可以返回一个非负整型
function getData() public view returns(uint256){
    return 5;
}
```