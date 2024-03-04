# Content/铸造NFT

在将TokenId与小猫信息关联之后，我们还需要为该TokenId创建对应的NFT。

在这一步，我们将调用ERC721中提供的***_mint***函数。这个函数需要两个参数：*NFT的主人*和*TokenId*。我们已经有了这两个信息，分别是参数***owner***和状态变量***_tokenIdCounter***。

**Syntax Review**

mapping

- 提示
    
    ```solidity
    _mint(owner, TokenId);
    ```