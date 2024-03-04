# Content/生成NFT信息

在定义完***mint***函数之后，我们需要做三件事情。

1. 更新***tokens**映射*
2. 更新***ownerTokens**映射*
3. 更新***tokenId***的值

首先我们更新***tokens**映射*，共分为两步：第一步，我们需要使用参数信息新建一个Token*结构体*，因为每一个Token表示一个NFT。

第二步，我们需要将此结构体赋值给tokenId对应的***tokens** 映射*，因为***tokens***是存储所有的NFT信息的变量。

在这里我们首先完成第一步，我们需要将NFT表示出来。而基于*函数*的*参数*，我们可以构建一个Token*结构体*来表示这些信息。

因此，在这个阶段，我们将根据*函数*的*参数*创建一个全新的Token实例，并将其暂时保存在内存memory中，以便后续操作能够方便地使用它。

> 选择memory的原因是，是因为将数据存储在memory 更省gas费。所以我们在不需要操作storage的时候，一般都使用memory来存储数据。
> 

**Syntax**

mapping,data location

- 提示
    
    ```solidity
    Token memory token = Token(_name, _desc, msg.sender);
    ```