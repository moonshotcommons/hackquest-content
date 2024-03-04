# Content/创建小猫并返回其对应的TokenId

有了基因信息后，我们可以调用***_createKitty***函数来创建小猫。

要创建一个小猫，我们需要将小猫的基础信息作为参数传给***_createKitty***函数。

> 具体来说，这个函数需要以下参数：猫妈妈的TokenId、猫爸爸的TokenId、迭代数、基因和猫主人。
> 

当创建初代小猫时，因为它是第一代并且是人为创建的，我们可以假设它没有父母。迭代数设为*0*，基因则是我们刚刚计算出的随机数。另外，由于是用户调用***createKittyGen0***函数来创建小猫，猫的主人应该是函数的调用者。

我们之前提到，***createKittyGen0***函数应返回新创建的小猫的TokenId。因此，我们可以调用***_createKitty***函数来获取新小猫的TokenId，并将这个值返回给调用者。

**Syntax**

return,function call

- 提示
    
    ```solidity
    return caculate_add(4, 5);
    ```