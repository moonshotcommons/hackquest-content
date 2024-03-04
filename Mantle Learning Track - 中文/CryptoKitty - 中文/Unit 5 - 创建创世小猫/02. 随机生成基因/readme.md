# Content/随机生成基因

在前面的步骤中，我们提到***createKittyGen0***函数需要随机生成小猫的基因，这个基因是一个uint256类型的变量。为此，我们需要一个**随机数**生成算法。

在Solidity中，常用的随机数生成方法涉及到两个内置函数：keccak256和abi.encodePacked。keccak256是一个哈希生成算法，能够将任意长度的输入转换为一个固定长度的bytes32类型的哈希值。由于不同的输入会产生不同的哈希值，我们只需确保输入字符串包含小猫的独特信息。

那么，如何构造这样的独特信息呢？我们可以使用abi.encodePacked函数来编码多种信息，如当前的时间戳、TokenId等具有唯一性的属性。由于这些属性对每只小猫都是独特的，将它们编码并通过keccak256进行哈希处理后，那么每个小猫就可以拥有属于自己的独特基因了。

**Syntax**

hash,abi.encodePacked

- 提示
    
    ```solidity
    //以下是一个根据时间戳和姓名生成随机数的示例
    uint256(keccak256(abi.encodePacked(timestamp, name)))
    ```