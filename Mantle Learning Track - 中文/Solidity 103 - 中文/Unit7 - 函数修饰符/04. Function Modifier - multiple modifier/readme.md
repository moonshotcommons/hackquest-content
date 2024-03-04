# Content/概念

### Concept

单个“函数”可以有多个“修饰符”。 修饰符按照它们出现的顺序执行。

- 比喻
    
    Solidity 函数中的多个修饰符就像不同检查点的安全许可层，其中每个修饰符代表在访问受保护区域（函数执行）之前必须授予的特定授权级别。
    
- 真实用例
    
    在这个合约中，***changeOwner***“函数”有两个“修饰符”：***onlyOwner***和***onlyAfterOneHour***。 ***onlyOwner*** 修饰符 限制该函数只能由所有者调用。 ***onlyAfterOneHour*** *modifier* 限制该函数只能在 *contract* 部署后一小时内调用。 “修饰符”按照列出的顺序执行。
    
    ```solidity
    contract MultiModifierContract {
      address public owner;
      uint public creationTime;
    
      constructor() {
        owner = msg.sender;
        creationTime = block.timestamp;
      }
    
      modifier onlyOwner {
        require(msg.sender == owner, "Only owner can execute.");
        _;
      }
    
      modifier onlyAfterOneHour {
        require(block.timestamp >= creationTime + 1 hours, "Function can only be called after one hour.");
        _;
      }
    
      function changeOwner(address _newOwner) public onlyOwner onlyAfterOneHour {
        owner = _newOwner;
      }
    }
    ```
    

### Documentation

当一个“函数”有多个“修饰符”时，它们以空格分隔，并按它们出现的顺序应用。

```solidity
function bid() public payable aboveMinimumBid beforeAuctionEnd {
    // Place the bid
}
```

### FAQ

- 多个修饰符如何一起工作，如果一个函数有多个修饰符，执行顺序是什么？
    
    当函数有多个修饰符时，它们按照它们在函数声明中出现的顺序应用。 每个修饰符必须在函数执行之前成功验证，从而创建一系列条件来共同确定函数是否可以继续。

# Example/示例代码

```solidity
pragma solidity ^0.8.0;

contract MyContract {
  address public owner;

  constructor() {
    owner = msg.sender;
  }

  modifier onlyOwner() {
    require(msg.sender == owner, "Only owner can call this function.");
    _;
  }

  modifier notNull(address newOwner) {
    require(newOwner != address(0), "New owner's address must not be zero.");
    _;
  }

  function changeOwner(address newOwner) public onlyOwner notNull(newOwner) {
    owner = newOwner;
  }
}
```