# Content/**给返回值赋值**

到目前为止，我们已经成功实现了通过TokenId检索相应NFT信息的功能。

接下来，我们要完成查询操作的最后一步：为函数的返回值赋值。

由于在*函数*定义时，*返回值*已经被命名，所以我们只需将*返回值*与*Token结构体*中的各个属性一一对应即可。

**Syntax**

variable

- 提示
    ```
    name = token.name;
    description = token.description;
    owner = token.owner;
    ```