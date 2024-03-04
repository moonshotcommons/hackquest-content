# Content/权限控制

现在是时候来实现这个函数功能了。

就像我们之前在定义***owner***状态变量时提到的，***mint***函数需要做一个权限控制。

我们将使用`require`语句检查调用者地址是否为***owner***记录的发行者，如果不是，则会调用失败，此次交易将回滚。

> 回滚意味着区块链的数据将恢复到此次交易发生前的状态。
> 

**Syntax**

Require, msg.sender

- 提示
```Solidity
require(owner == msg.sender);
```