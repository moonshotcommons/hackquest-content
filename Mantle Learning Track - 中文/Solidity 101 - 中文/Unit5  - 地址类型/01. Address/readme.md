# Content/概念

### Concept

这节我们学习的变量类型是地址（`address`）类型。 *地址*是以太坊区块链上账户或智能合约的唯一标识符。

- 比喻
    
    *地址*类似于唯一的用户名或帐户号，有助于识别和与以太坊平台上的个人用户或智能合约并与之交互。
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/47d6b6f3-a287-4d16-8ce7-201e0f72bca6/Untitled.png)
    
- 真实用例
    
    在ERC20的[transfer](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/8186c07a83c09046c6fbaa90a035ee47e4d7d785/contracts/token/ERC20/ERC20.sol#L118)函数中，使用address类型的to来表示要转账的接收方地址。
    
    ```solidity
    function transfer(address to, uint256 value) public virtual returns (bool) {
        address owner = _msgSender();
        _transfer(owner, to, value);
        return true;
    }
    ```
    

### Documentation

要定义一个*地址*，我们只需要使用`address`关键字。

```solidity
//定义
address address1 = 0x35701d003AF0e05D539c6c71bF9421728426b8A0;

//在以太坊中，每个地址都有一个成员变量，即地址的余额balance
//余额以 uint 形式存在，因为它永远不可能为负值
uint balance = address1.balance;
```

地址占20个`字节`，一个字节有8个`bit`,所以地址共有160个*bit*，一个字节需要两个十六进制数表示，所以需要40个十六进制数表示一个地址。

### FAQ

- 不同的地址之间有区别吗？
    
    *地址*分为两类：`账户地址`或`合约地址`。
    
    **账户地址**
    
    它是由用户创建的用于接收或发送资金的*地址*，由用户控制，也称为钱包。如果你不熟悉此概念，请参考 Metamask。
    
    **合约地址**
    
    与“账户地址”相反，“合约地址”由`合约`（程序）控制。将*合约*放在以太坊上时，系统会为它生成一个独特的地址。其他人通过这个地址与合约进行交互。
# Example/示例代码

```solidity
pragma solidity ^0.8.0;

contract AddressArray {
	address b = 0x5B38Da6a701c568545dCfcB03FcB875f56beddC4;
	uint balance = b.balance;
}
```
