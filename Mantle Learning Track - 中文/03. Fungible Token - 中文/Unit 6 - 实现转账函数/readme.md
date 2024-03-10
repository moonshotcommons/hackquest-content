# Content/引文

截至目前，我们已经完成了：

- 代币的铸造
- 代币余额的查询

我们的代币系统已经初见雏形了，但要成为一个真正意义上的代币系统，还差一个交易功能，也就是转账。

在本节中，我们将实现*代币合约*的最后一个功能：**转账**。 转账包括这里的几个步骤

1. 首先我们需要判断转账者的余额**是否大于**要转账的金额
2. 然后我们需要通过映射分别获取转账者和接收者余额
3. 然后在转账者的映射上减去要转账的金额
4. 在收款者的映射上加上转账的金额
5. 更新所有与金额有关的变量后，转账就完成了。

那么此时转账就完成了。 在本节结束时，我们将能够在 Remix 中部署和检查我们的转账结果

# Example/ Code

```solidity
pragma solidity 0.8.17;

contract MyToken {
    mapping (address => uint256) private balances;
    uint256 public totalSupply;
    address private owner;

    constructor(){
				owner = msg.sender;
		}
    
    function mint(address recipient, uint256 amount) public {
        require(msg.sender == owner);
        balances[recipient] += amount;
        totalSupply += amount;
    }

    function balanceOf(address account) public view returns (uint256) {
				return balances[account];
		}
}
```

