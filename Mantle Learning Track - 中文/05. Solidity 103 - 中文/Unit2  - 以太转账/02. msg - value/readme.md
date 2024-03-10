# Content/概念

### Concept

我们之前在Solidity 101已经学习了*msg.sender*，它们用于获取与当前函数交互的地址信息。现在让我们继续学习msg的另一个全局变量：msg.value。

*msg.value*用于获取当前函数调用时传递给合约的以太币（Ether）数量。它表示当前函数调用中附带的以太币金额，通过读取*msg.value*的值，合约可以确定用户向其发送的以太币数量，进而执行相应的逻辑。

- 比喻
    
    在现实生活中，当我们支付购买商品时，会交换一定数量的货币。同样，在区块链世界中，当用户向智能合约发送交易时，*msg.value*就代表着这笔交易中需要转移的以太币金额。
    
    ![ABECE149-EF21-4216-AEBF-9CA75EE7A59E.jpeg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d1eec182-fa52-4565-84d9-b7db610b6c9c/ABECE149-EF21-4216-AEBF-9CA75EE7A59E.jpeg)
    
- 真实用例
    
    还是刚刚的***ERC2771Forwarder***合约，由于该函数希望有人传递ETH进行调用，就需要知道调用者传递的ETH数量是多少，这时就需要*msg.value*来获取。
    
    ```solidity
    function executeBatch(
        ForwardRequestData[] calldata requests,
        address payable refundReceiver 
    ) public payable virtual {
        ...
        if (requestsValue != msg.value) {
            revert ERC2771ForwarderMismatchedValue(requestsValue, msg.value);
        }
        ...
    }
    ```
    

### Documentation

`msg.value`作为全局变量，直接使用。

```solidity
//在这里我们使用msg.value获取到了调用者附加的以太币价值，并将值赋值给了value变量。
uint256 value = msg.value;
```

### FAQ

- msg.value的单位是？
    
    *msg.value*的单位是Wei，是以太坊最小的货币单位。1 Eth = 10^18 Wei。

# Example/示例代码

```solidity
pragma solidity ^0.8.0;

contract Example {
  uint256 public totalAmount;

  function pay() public payable {
    // 增加传递的以太币到总金额
    totalAmount += msg.value;
  }
}
```
