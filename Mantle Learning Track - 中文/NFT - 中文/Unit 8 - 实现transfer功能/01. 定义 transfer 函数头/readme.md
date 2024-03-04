# Content/**定义 transfer 函数头**

让我们开始定义***transfer***的函数头，为了完成转账，理论上我们需要知道：发件人，接受者和要转移的TokenId三个参数，但由于*函数调用者*可以被视为发送者，我们可以使用 msg.sender 语法获取它。

因此，在这里我只需要接收者和要转移的TokenId两个*参数*。

在可见性的选择上，由于我们希望无论在合约内外，都可以调用该*函数*进行NFT的转移，所以我们使用`public`

**Syntax**

function,scope,msg.sender

- 提示
    ```
    //例如这里，我们通过指定appleId，将该apple转移给recipient
    function transferApples(address recipient, uint256 appleId) public {

    }
    ```