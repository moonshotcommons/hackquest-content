# Content/**参数检查**

在前面的步骤中，我们定义了一个带有参数的函数。现在是时候考虑是否需要对*参数*进行检查了。

这里的*参数*是 NFT 的TokenId。我们应确保 TokenId的值在我们已经铸造的 NFT 范围内，也就是 TokenId必须大于*1*且小于 ***nextTokenId***。

如果传入一个“越界”的 TokenId进行查询，可能会导致后续的查询过程出现异常。因此，*参数*检查在这里是非常必要的。

**Syntax**

require

- 提示
    ```
    require(i > 1, "error");
    ```