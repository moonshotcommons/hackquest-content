# Content/**获取发送者地址的钱包**

在删除之前，我们肯定需要先获取到钱包，并将其存储在storage当中，以供后期的修改操作。

那么我们在这里就需要在***ownerTokens**映射*中根据***accont***去获取钱包这个*uint256*的*数组*。

**Syntax**

array ,data location

- 提示
    
    ```solidity
    uint256[] storage arr = ownerTokens[account];
    ```
