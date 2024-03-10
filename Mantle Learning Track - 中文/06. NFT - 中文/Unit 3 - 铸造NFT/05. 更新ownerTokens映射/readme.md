# Content/**更新**ownerTokens**映射**

接着，我们更新***ownerTokens**映射*，同样需要两步：第一步，我们需要在***ownerTokens**映射*中获取该*地址*所持有的tokenId数组，因为该*映射*存储着每个地址对应的tokenid数组。

第二步，将铸造出的NFT的**tokenId**添加到该*地址*所持有的tokenId数组中。

**Syntax** 

mapping,push,msg.sender

- 提示
    ```
    owners[msg.sender].push(id);
    ```