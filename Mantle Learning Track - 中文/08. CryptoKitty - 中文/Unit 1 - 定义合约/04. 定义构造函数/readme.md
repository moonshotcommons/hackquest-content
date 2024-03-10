# Content/定义构造函数

在定义合约之后，不要忘记 ERC721 有一个**构造函数**，它需要代币的*名称*和*符号*作为参数来初始化ERC721。

现在我们将定义我们自己的 *constructor* 来 **初始化**ERC721。

**Syntax**

constructor inherited

- 提示
    
    ```solidity
    constructor() ERC721("name", "symbol") {}
    ```