# Content/定义breed函数

我们现在来定义***breed***函数。首先，你需要明白这个函数的目的：它是为了根据指定的猫妈妈和猫爸爸孕育出下一代小猫，而这只小猫的基因与其父母有关。

因此，我们需要为猫爸和猫妈定义两个*uint256*类型的参数，这样我们可以查询他们的基本信息。

关于函数的可见性，我们选择`public`，因为我们希望这个函数无论在合约内部还是外部都可以被调用。

**Syntax**

function,scope

- 提示
    
    ```solidity
    function breed(uint256 momId, uint256 dadId) public returns (uint256) { }
    ```