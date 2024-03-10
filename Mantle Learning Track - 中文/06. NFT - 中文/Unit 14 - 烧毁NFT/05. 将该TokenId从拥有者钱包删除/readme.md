# Content/**将该TokenId从拥有者钱包删除**

接下来就开始删除步骤了~

我们首先需要把该NFT从其拥有者的钱包中删除，还记得我们在上一节中专门定义了一个函数来实现这个功能吗？

现在又派上用场了！让我们直接将**调用者**和***_tokenId***作为参数调用该*函数*吧！

**Syntax** 

variable

- 提示
    
    ```solidity
    //调用删除函数
    deleteById(msg.sender, id);
    ```