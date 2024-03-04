# Content/概念

### Concept

在这一节中，我们来学习solidity中一个特殊的结构——事件。

在Solidity中，*事件*（*Event*）是一种用于在智能合约中发布通知和记录信息的机制。它可以在合约执行期间发出消息，允许外部应用程序监听并对这些消息做出响应。

- 比喻
    
    事件可以被认为是合约的公告板，可以向外部应用程序广播重要的信息。
    
    ![Untitled](./img/1-1.pngg)
    
- 真实用例
    
    在IERC20中，定义了一个***[Transfer](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/token/ERC20/IERC20.sol#L16C77-L16C77)***事件，该事件记录了转账的发起者和接收者，以及转账的金额信息。
    
    ```solidity
    event Transfer(address indexed from, address indexed to, uint256 value);
    ```
    

### Documentation

在solidity中我们使用`event`关键字来声明一个事件，其后是事件名，随后用括号把参数括起来。

```solidity
//在这里我们定义了一个名为EventName的事件，其有parameter1和parameter2两个参数。
event EventName(
  uint256 parameter1,
  uint256 parameter2
);
```

### FAQ

- 什么时候需要使用事件？
    
    假设你是一个电商平台的管理员，你有一个智能合约来处理用户下单的过程。当有人下单时，你需要通知所有相关方，例如买家、卖家和物流公司。
    
- 如何使用事件？
    1. 定义一个名为***Order***的事件，里面包括下单者的地址，下单的物品，下单的数量。
        
        ```solidity
        event Order(address sender, string goods, uint count);
        ```
        
    2. 在有人下单的时候广播***Order***事件，这样所有人都可以收到下单者的地址，下单的物品，下单的数量这三个信息。

# Example/示例代码

```solidity
pragma solidity ^0.8.0;

contract EventContract {
  // 定义事件，记录发送者地址和新的值
  event ValueUpdated(address sender, uint newValue);

  uint public value;
  // 更新值并触发事件
  function updateValue(uint _newValue) public {
    value = _newValue;
    //发出事件，我们将在下一章的内容中讲到
    emit ValueUpdated(msg.sender, _newValue);
  }
}
```
