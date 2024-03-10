# Content/概念

### Concept

这一章我们来学习一个Solidity中的特殊函数 - receive。

receive 函数只用于处理接收ETH，一个合约最多只有一个，而且不能有任何的参数，不能返回任何值，必须包含external和payable。

- 比喻
    
    简单来说，可以把receive理解成存钱窗口。你只能把钱放进去，也不能发送任何的消息，很多时候*receive*只是单纯的收钱窗口。
    
- 真实用例
    
    在 ***[Governor](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/governance/Governor.sol#L82)*** 合约中，我们使用receive函数来收取管理者可以开支的Ether。
    
    ```solidity
    /**
    * @dev Function to receive ETH that will be handled by the governor (disabled if executor is a third party contract)
    */
    receive() external payable virtual {
      if (_executor() != address(this)) {
          revert GovernorDisabledDeposit();
      }
    }
    ```
    

### Documentation

使用`receive`关键字定义的一种特殊函数，必须包含`external`和`payable`。

```solidity
//这里我们定义一个空的receive函数。
receive() external payable { ... }
```

### FAQ

- *receive* 函数是必须的吗
    
    不是的，你可以选择定义*receive*也可以不定义，但是如果不定义，在合约收到转账时可能会报错。
    
- *receive* 除了不能有参数和返回值之外和其他的函数还有什么区别？
    
    receive 限制只能消耗2300 gas，这个数量的gas基本就只能收个Ether
    

# Example/示例代码

```solidity
pragma solidity ^0.8.0;

contract ContractA {
  bool public flag;
  //receive 函数
  receive() external payable {
    flag = true;
  }
}

contract ContractB {
  function callReceive(address _contract) external payable {
    //receive会被执行，是因为我们发送了Eth，并且没有带任何数据（“”为空）
		(bool suc,) = _contract.call{value: 1}("");
    require(suc, "call fail");
  }
}
```