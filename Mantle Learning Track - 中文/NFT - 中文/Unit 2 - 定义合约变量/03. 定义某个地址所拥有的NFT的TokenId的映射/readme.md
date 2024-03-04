# Content/**定义一个整型变量作为指针**

在本章中，我们的目标是查询特定地址所拥有的所有NFT。然而，仅仅依靠我们目前定义的***Token**结构体*和***tokens**映射*是无法实现的。

我们需要一个类似于钱包的变量，该*变量*需要将*地址*和其拥有的所有NFT联系起来。

这个*变量*可以被看作是一个*映射*关系，它将**地址**映射到一个**TokenId 数组**上。

为了更好的理解这个*变量*，你可以把它想象成从*地址*到钱包的*映射*，而钱包的数据结构就是tokenId数组。

> 在后续教程中，我们会反复使用钱包来代指TokenId数组
> 

因此我们首先需要定义一个**映射**。

**Syntax**

mapping,array,adress

- 提示
    
    ```solidity
    contract Example{
        //例如这里的NFTs就可以记录每个地址持有的NFT的tokenId数组
        mapping (address => uint256[]) private NFTs;
    }
    ```