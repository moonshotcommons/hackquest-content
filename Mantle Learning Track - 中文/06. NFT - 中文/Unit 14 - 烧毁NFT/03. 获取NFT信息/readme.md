# Content/**获取NFT信息**

在完成参数的检查后，我们就可以通过TokenId去检索NFT了，**tokens***映射*为我们提供了一个非常便捷的查询方式。

因为我们在后续的步骤中需要改变该NFT的信息，我们需要将查询到的NFT保存在storage里。

> 如果存在memory里，那么后续的修改将只存在于内存当中，而不会修改合约的状态。
> 

**Syntax**

mapping,variable

- 提示
    
    ```solidity
    NFT storage nft = NFTs[TokenId];
    ```