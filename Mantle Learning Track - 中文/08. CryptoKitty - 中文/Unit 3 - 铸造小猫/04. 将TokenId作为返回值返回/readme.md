# Content/将TokenId作为返回值返回

到现在为止，我们就已经完成了小猫的创建，具体来说我们完成了小猫信息的创建，将小猫信息和**TokenId**一一对应，并铸造了NFT。

最后，我们只需要将**TokenId**作为返回值返回，并将**TokenId**自增，使其指向下一个要铸造的NFT的**TokenId**即可。

**Syntax Review**

mapping

- 提示
    
    ```solidity
    //在这个示例中，我们返回的TokenId仍然为1，但同时也完成了TokenId的自增。
    TokenId = 1;
    return TokenId++;
    ```