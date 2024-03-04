# Content/获取猫爸猫妈信息

非常好，现在让我们进入***breed***函数真正的逻辑吧。

为了孕育出下一代小猫，我们就需要获取猫爸和猫妈的基础信息，而该基础信息是存储在***kitties***这个映射中。

我们可以直接使用参数中的*momId*和*dadId*在***kitties***映射中查询到指定TokenId的***Kitty***结构体。

在这一步中，我们将分别获取猫妈和猫爸对应的***Kitty***结构体。

在Solidity中，当处理结构体时，我们需要指定其存储位置。由于不需要改变猫妈和猫爸的信息，我们选择存储在memory当中，这会节省不少*gas*消耗。

**Syntax**

mapping

- 提示
    
    ```solidity
    //例如这里就获取了studentId对应的students映射中存储的Student结构体
    Student memory a = students[studentId];
    ```