# Content/**定义mint函数**

定义一个名为***mint***的公开函数，该函数需要知道被铸造NFT的**name**以及**description**。

> owner字段可以通过msg.sender来读取
> 

因此我们定义两个参数分别为

1. *string*类型的变量 ***_name***
2. *string*类型的变量***_description***

<aside>
💡 由于string类型作为参数时必须指定存储位置，由于我们不涉及storage的修改，所以我们在这里选择memory。

</aside>

**Syntax**

function

- 提示
    ```
    提示
    // 这里给出了mint的标准定义
    // 请注意string等变长类型在作为参数输入时必须指定他的存储位置
    // 例如这里我们只需要读取参数内容，所以使用memory
    function mint(string memory _name, string memory _description) public {}
    ```