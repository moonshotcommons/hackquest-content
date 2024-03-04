# Content/**参数检查**

这里的入参又是TokenId，还记得我们之前的部分中，对于TokenId作为*入参*的检查吗？

我们应该确保TokenId的值在我们已经铸造的NFT当中，也就是TokenId必须是大于*1*但是小于***nextTokenId***的。

**Syntax**

require,address

- 提示
    
    ```solidity
    require(TokenId > 1);
    ```