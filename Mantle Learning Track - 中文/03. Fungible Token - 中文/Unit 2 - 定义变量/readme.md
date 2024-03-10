# Content/引文

在上一节中，我们已经完成了合约的初步搭建。在这一小节，我们将代币合约的数据结构进行进一步的完善。

# Example/ Code
```solidity
    pragma solidity 0.8.17;
    contract MyToken {

	address private owner;
        constructor(){
        owner = msg.sender;
        }
    }
```