# Content/概念

### Concept

在之前，我们学习了`revert`语句的异常处理机制.

在这一节中，我们将学习一种**自定义**的错误类型：错误(`error`)，用于表示合约执行过程中的异常情况。它可以让开发者定义特定的错误状态，以便在合约的执行过程中进行特定的异常处理。

![Untitled](./img/2-1.png)

- 比喻
    
    error就好像老师批阅卷子时给我们明确的指出哪个步骤错了，而不是笼统的告诉我们这个题写的有问题。
    
- 真实用例
    
    在OpenZepplin的***[Ownerble](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/access/Ownable.sol#L63C1-L68C1)***合约中，使用error来表示身份验证失败的错误类型。
    
    ```solidity
    error OwnableUnauthorizedAccount(address account);
    function _checkOwner() internal view virtual {
        if (owner() != _msgSender()) {
            revert OwnableUnauthorizedAccount(_msgSender());
        }
    }
    ```
    

### Documentation

在Solidity中，定义错误类型使用关键字`error`，随后是参数**。**

```solidity
//使用error关键字定义了一个名为***MyCustomError***的自定义错误类型
//并指定错误消息类型为string 和 uint。
error MyCustomError(string message, uint number);

function process(uint256 value) public pure {

		//检查***value***是否超过了*100*。如果超过了限制，我们使用revert语句抛出自定义错误
		//并传递错误消息"*Value exceeds limit*" 和***value***。
		if (value >100) revert MyCustomError("Value exceeds limit",value);

}
```

### FAQ

- 使用error的好处？
    
    有时我们需要定义一个错误的类型，让很多个地方报错信息一致，这就是error的作用。
    
    使用error可以同时提高代码的可读性以及可维护性。
    
- error可以在合约外定义吗？
    
    可以 error可以在`contract{…}`外定义。

# Example/示例代码

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Bank {
    mapping(address => uint) private balances;

    //自定义错误类型InsufficientFunds
    error InsufficientFunds(uint requested, uint available);
    
    function deposit() public payable {
        balances[msg.sender] += msg.value;
    }

    function withdraw(uint amount) public {
        if (amount > balances[msg.sender]) {
						//回滚交易，并且提交自定义错误类型InsufficientFunds
            revert InsufficientFunds(amount, balances[msg.sender]);
        }
        balances[msg.sender] -= amount;
        payable(msg.sender).transfer(amount);
    }

    function getBalance(address account) public view returns (uint) {
        return balances[account];
    }
}
```