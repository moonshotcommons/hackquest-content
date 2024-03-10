# Content/创建新小猫

在算出了小猫的基因和迭代数后，我们已经有了生成一只新的猫所需要的所有信息。具体来说：

1. 猫爸的TokenId - ***dadId***
2. 猫妈的TokenId - ***momId***
3. 基因 - ***newGenes***
4. 迭代数 - ***newGeneration*** 
5. 小猫主人 - ***msg.sender***

还记得我们在之前定义的***_createKitty***函数吗？它又可以派上用场了，在这里我们只需要将上述信息作为参数传入***_createKitty***函数调用即可。

**Syntax Review**

function call

- 提示
    
    ```solidity
    create(someMessage);
    ```