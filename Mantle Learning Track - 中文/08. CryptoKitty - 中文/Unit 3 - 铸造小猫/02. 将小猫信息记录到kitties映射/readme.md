# Content/将小猫信息记录到kitties映射

在***_createKitty***函数中，首先我们需要将小猫的信息存储到新创建的***kitties***映射中。

我们已经通过参数获得了以下信息：

1. 猫妈妈的TokenId
2. 猫爸爸的TokenId
3. 迭代数
4. 基因
5. 猫主人

为了创建一个完整的***Kitty***结构体，我们还需要一个属性：***birthTime***，即小猫的出生时间。在区块链中，我们可以使用block.timestamp语法来获取当前区块的时间。

一旦我们拥有了***Kitty***结构体中的所有信息，就可以创建一个新的小猫。接下来，我们只需将要铸造的NFT的TokenId与这个新小猫关联起来即可。

**Syntax**

mapping

- 提示
    
    
    ```solidity
    //例如这里就将studentId和学生信息一一对应起来
    students[studentId] = Student(name,classId);
    ```