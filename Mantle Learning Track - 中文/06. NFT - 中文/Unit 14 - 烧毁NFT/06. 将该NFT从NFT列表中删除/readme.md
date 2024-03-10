# Content/**将该NFT从NFT列表中删除**

我们现在删除了NFT在钱包中的信息，而在*合约*中，还有一个NFT的列表***_tokens**映射*中的信息没有删除。

映射的删除就很简单了，直接使用`delete`语句就行

**Syntax** 

delete mapping

- 提示
    
    ```solidity
    delete map[key];
    ```