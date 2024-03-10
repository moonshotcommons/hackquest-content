# Content/**获取指定NFT的信息**

在完成参数检查后，我们可以开始进行真正的查询操作。

回想一下之前我们定义的***tokens** 映射*。这个*映射*用于将TokenId与NFT详细信息关联起来。

现在，我们需要通过***tokens** 映射*查询传入*参数**_tokenId***对应的NFT详细信息。

并将该NFT的详细信息存储在该*函数*的memory当中，以后续操作中将信息*返回*。

> 选择*memory*的原因是，是因为将数据存储在*memory*更省gas费。所以我们在不需要操作storage的时候，一般都使用*memory*来存储数据。
> 

**Syntax**

mapping,data location

- 提示
    ```
    Token memory token = tokens[id];
    ```