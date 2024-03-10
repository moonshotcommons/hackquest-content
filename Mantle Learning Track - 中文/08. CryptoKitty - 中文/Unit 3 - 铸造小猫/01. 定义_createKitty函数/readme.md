# Content/定义_createKitty函数

现在，我们开始定义***_createKitty***函数。该函数的主要目的是提供一个公共方法，用于根据给定的小猫信息铸造一个NFT，并在合约中记录小猫信息，使其与TokenId一一对应。

***_createKitty***函数接受五个参数：猫妈妈的TokenId、猫爸爸的TokenId、迭代数、基因和猫的主人。这五个参数将用于初始化NFT结构体。其中，猫的主人信息是为了确保新铸造的NFT被分配给正确的主人。

由于***_createKitty***函数是设计为合约内部的通用功能，我们将其可见性设置为`private`。

正如上一节所提到的，该函数还需要返回新创建的小猫NFT的TokenId，因此我们需要一个*uint256*类型的返回值。

**Syntax**

function, scope, return

- 提示
    
    ```solidity
    //例如这里我们将基因和主人信息传入create函数中，且有一个uint256类型的返回值
    function create(uint256 genes, address owner) private returns (uint256) { }
    ```