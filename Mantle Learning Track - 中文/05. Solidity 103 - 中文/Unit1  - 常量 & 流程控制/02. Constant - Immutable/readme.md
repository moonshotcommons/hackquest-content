# Content/概念

### Concept

刚刚我们学习了常量的其中一种定义方式：*constant*。

在这一节中，我们将学习另一种不可变的变量的定义方式*immutable*：immutable与常量（constant）不同，immutable 变量的值可以在部署合约时确定，但在部署后无法更改。

换句话说immutable修饰的变量可以在构造函数中对其赋值，且赋值后不可更改。而constant在声明时就必须被赋值。

- 比喻
    
    immutable就像是身份证号码，在你出生或获得身份证时，会分配一个唯一的身份证号码。这个号码在之后的生活中是不能更改的。
    
- 真实用例
    
    在OpenZepplin中的[***GovernorVotes***](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/governance/extensions/GovernorVotes.sol#L15)合约中，将治理代币定义为*immutable*，并在构造函数中通过初始化传参为其赋值，随后该值将不可更改。
    
    ```solidity
    IERC5805 public immutable token;
    
    constructor(IVotes tokenAddress) {
        token = IERC5805(address(tokenAddress));
    }
    ```
    

### Documentation

在定义immutable变量时，我们需要在变量类型和变量名中间使用关键字`immutable`。

```solidity
//在这里定义了一个immutable的变量num
uint256 immutable num;

//为了给immutable变量赋值，你需要在声明时或者在构造函数中进行初始化。\
//一旦赋值后，它的值就无法更改。
constructor(uint256 _num) {
  num = _num;
}
```

<aside>
💡 和constant一样，immutable只能用于状态变量的定义。这是因为immutable修饰的变量也会硬编码到合约的字节码中。

</aside>

<aside>
💡 你只可以在构造函数中对immutable的变量赋值

</aside>

### FAQ

- 为什么使用Immutable？
    
    其相较于*constant*可以在部署时再为变量赋值，而不是在写合约时，这使得*immutable*更加灵活。
    
    immutable 变量在部署时将其硬编码到合约字节码中。这使得访问 immutable 变量的成本较低，因为它们在部署后不需要从*storage*中读取。

# Example/示例代码

```solidity
pragma solidity ^0.8.0;

contract Example {
  //在这里定义了一个immutable变量，其值需要在构造函数中定义。
  address immutable public token;

  constructor(address _tokenAddress) {
    token = _tokenAddress;
  }
}
```
