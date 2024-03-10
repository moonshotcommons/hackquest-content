# Content/引文

在上一节中，我们实现了代币的铸造功能。而用户怎么才能确定自己刚刚的铸造是成功且正确的呢？通常用户会去查询账户的余额，那么在本节中，我们将实现代币合约的第二个功能：**查询余额**。 查询包括这里的几个步骤：

1. 首先我们需要接收一个账户地址作为入参。
2. 我们将要在***balances***映射中查找该地址对应的余额。
3. 将该余额作为函数返回值返回。

那么此时查询余额就完成了。 在本节结束时，我们将能够在 Remix 中通过此函数查询任何*地址*的余额

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

}
```

