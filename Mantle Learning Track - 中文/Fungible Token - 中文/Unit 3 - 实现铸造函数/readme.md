# Content/引文

在上一节中，我们已经将代币合约的数据结构进行了完善。在这一小节，我们将实现 *代币合约*的第一个*功能*：**铸造**代币。 

1. 在铸造代币之前，我们需要检查函数的调用者是否是代币的发行者，以确保只有发行者可以随意铸造代币。
2. 每次我们铸造代币时，我们都要指定接收代币的账户地址和代币数量。
3. 更新所有与金额有关的变量后，铸币就完成了。

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
}
```