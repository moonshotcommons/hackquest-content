# Content/**定义getTokensByOwner 函数**

为了实现查询功能，我们刚刚定义了一个名为***ownerTokens***的映射，现在一切准备就绪。

接下来，我们将创建一个函数，用于查询指定地址所拥有的所有NFT。这个功能提供了一种简单的方式来跟踪你所拥有的NFT。

既然我们要实现查询，那么我们需要一个参数来表示要查询的账户*地址*。

查询的返回值应该是该*地址*所拥有的所有NFT的TokenId，因此*返回值*应该是*uint256*类型的数组。

**Syntax**

return,calling,address

- 提示
    ```
    function getTokensByOwner(address _owner) public view returns (uint256[] memory) { }
    ```