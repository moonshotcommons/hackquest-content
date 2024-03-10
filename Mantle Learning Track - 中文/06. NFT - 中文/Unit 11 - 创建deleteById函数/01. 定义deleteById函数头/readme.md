# Content/**定义deleteById函数头**

首先，我们需要来定义***deleteById***函数头。

由于该*函数*需要删除指定地址的钱包中某个TokenId。所以我们需要两个入参，分别是账户地址和TokenId。

在*函数*的可见性方面，由于该*函数*可以删除任何人的NFT，因此我们将其定义为`internal`，只有合约内部的其他函数可以调用它来实现删除的功能。

**Syntax** 

function internal

- 提示
    
    ```solidity
    function deletefunction(address addr, uint256 TokenId) internal { }
    ```
