# Content/定义mint函数

到目前为止，我们已经将代币合约的所有变量定义完成，且通过构造函数确定了代币的发行者。现在就可以来定义***mint***函数了！

首先，我们需要理解该函数的作用。 该函数的目的是给目标地址铸造指定数量的代币。

因此，我们在定义函数时需要做的是指定铸造代币的数量和一个接收者地址。当然，因为***mint**函数功能*的特殊性，权限控制是必不可少的。

**Syntax**

Function parameters

- 提示
    
    ```solidity
    //例如这个giveApple函数，要想给某个地址发苹果，我们就需要知道他的地址和需要分发的数量
    function distributeApple(address recipient, uint256 amount) public {
           
    }
    ```