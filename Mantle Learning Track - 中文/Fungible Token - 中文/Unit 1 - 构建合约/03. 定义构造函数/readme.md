# Content/定义构造函数

我们之前提到***owner***字段用于定义为代币的发行者，也就是合约的部署者。

而在合约中确定部署者的唯一方式是在构造函数中使用`msg.sender`语法，这是因为构造函数的特殊性：构造函数只能在合约部署时执行一次，执行时默认的调用者为合约的部署者。

所以我们需要定义一个构造函数以确定代币的发行者。

**Syntax**

Constructor msg.sender

- 提示
    ```solidity
    constructor(){
    owner_address = msg.sender;
    }
    ```