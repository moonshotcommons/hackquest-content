# Content/记录当前NFT的tokneId

刚刚我们创建了要铸造的NFT的结构体，接下来我们来完成第二个步骤：将此*结构体*赋值给tokenId对应的***tokens**映射*。

而tokenId我们还未知，如何获取呢？

还记得我们的状态变量***nextTokenId***吗？它永远指向下一个要铸造的NFT的tokenId，那么我们这次要铸造的NFT的tokenId就是***nextTokenId***。

因此我们先将其存储到**局部变量**，也就是 memory 当中。

> 这么做有两个目的：①避免后续的操作中反复读取 storage*变量*（省gas）②这个memory的值将作为该NFT的tokenId的唯一标识，因为***nextTokenId***会在后续的步骤中指向下一个要铸造的NFT。
> 

**Syntax**

variable

- 提示
    
    ```solidity
    uint256 a = b;
    ```