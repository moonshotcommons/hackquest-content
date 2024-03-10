# Content/定义transfer函数

刚刚我们提到这是一个用于转账的函数，而要完成转账，我们需要知道：

- 转款者
- 收款者
- 转账金额

按理来说，我们需要三个入参，但是由于函数的调用者可以被认为是转款者，我们可以通过`msg.sender`语法获取。

所以实际上在***transfer***函数中我们只需要两个入参，收款者和转账金额。其中，收款者是一个地址类型，所以我们用`address`类型的变量；金额是一个非负的数，由于solidity不支持小数，所以我们只能选择无符号整型来表示。

函数的可见性我们选择`public`，因为我们希望无论是在合约内还是在合约外，都能访问该函数来进行转账。

**Syntax**

function scope ,parameters

- 提示
```solidity
//例如这个transferApples函数，可以实现用户与用户之间的苹果转移
function transferApples(address recipient, uint256 amount) public {

}
```