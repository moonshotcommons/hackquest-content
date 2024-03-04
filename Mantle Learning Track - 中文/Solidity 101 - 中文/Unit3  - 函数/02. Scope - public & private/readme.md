# Content/概念

在编写合约时，某些情况下合约中的特定功能需要与其他合约共享，此时我们可以使用`external`关键词。

- 比喻
    - `external` 好比一个公共图书馆，所有人都可以进去，但只有在开放时间才能进入。任何人都可以读书，但他们不能在图书馆里进行私人活动。（仅能使用`external`的函数功能）
- 真实用例
    
    在OpenZepplin的[***GovernorTimelockControl***](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/governance/extensions/GovernorTimelockControl.sol#L25) 合约中，定义了一个***[updateTimelock](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/governance/extensions/GovernorTimelockControl.sol#L145C14-L145C28)***的函数供外部用户或合约使用。
    
    ```solidity
    function updateTimelock(TimelockController newTimelock) external virtual onlyGovernance {
            _updateTimelock(newTimelock);
    }
    ```
    

### Documentation

要定义一个外部用户或其他合约能使用的*函数*，我们使用关键字 `external`，并将其放在*函数* 参数之后。

<aside>
💡 在本合约中使用时必须加上`this`关键词。

</aside>

```solidity

   function aa() external{}

   this.aa();
```

### **FAQ**

- 状态变量可以用external定义吗？
    
    `external`不能用于定义变量。
    
- 接口合约的函数可见性有什么特殊要求吗？
    
    接口合约中的*函数*都必须是`external`的。

# Example/示例代码

```solidity
contract A {

    uint public result;

    function aa(uint a) external {
        result = a + 1;
    }

    function b(uint b) public {
         this.aa(b);
    }
}
```
