# Content/定义createKittyGen0函数

非常好！在上一章中，我们已经定义了所需的变量。现在，让我们开始创建一个初代小猫。

首先，我们要定义一个名为***createKittyGen0***的函数。理解这个函数的目的是关键：它的任务是随机生成一个初代小猫。这个小猫的基因是随机的，父母信息为空，迭代数为*0*，出生时间则是当前区块的时间戳。这些组成了初代小猫的基本信息。

我们希望用户在创建随机的初代小猫后能知道自己创建的小猫的TokenId，因此这个函数需要返回一个值，即新创建的小猫的TokenId。

关于函数的可见性，我们选择`public`，因为我们希望这个函数可以在任何地方被调用，以创建一个初代小猫。

**Syntax**

function, scope, return

- 提示
    
    ```solidity
    function createKittyGen0() public returns (uint256) { }
    ```