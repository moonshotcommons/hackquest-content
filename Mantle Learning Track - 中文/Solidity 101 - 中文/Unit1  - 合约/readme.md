# Content/概念

### Concept

在上一节中，我们学习了如何定义编译器的版本。

那么现在让我们来学习如何定义一个合约：使用关键字 `contract` 定义合约，一个 Solidity 的 **.sol** 文件可以包含一个或多个 contract。

合约可以完全透明的存储数据和执行逻辑。

- 比喻
    
    智能合约就像是一份自动执行的合同，但不是由法律机构执行，而是由区块链网络上的计算机节点执行。
    
- 真实用例
    
    在Uniswap当中，使用`contract`关键字定义了一个[***UniswapV2Pair***](https://github.com/Uniswap/v2-core/blob/ee547b17853e71ed4e0101ccfd52e70d5acded58/contracts/UniswapV2Pair.sol#L11)合约。
    
    ```solidity
    contract UniswapV2Pair{ }
    ```
    

### Documentation

要定义一个 *合约*，我们使用关键字 `contract`，后面跟上合约的名称。

```solidity
contract Name { }
```

<aside>
💡 对于合约的命名，我们建议遵循“大驼峰”的命名规范，“大驼峰”是指每个单词的首字母都大写，例如：MyContract

</aside>

### FAQ

- 从代码的角度怎么理解contract？
    
    它类似于面向对象编程中的类。
    
    智能合约的代码逻辑包含了一系列函数和事件，用于定义合约的行为和功能。和其他编程语言不同的是，每一个contract对应着一个地址，且不可更改。
    
# Example/示例代码
```solidity
pragma solidity 0.8.17;

// 定义了一个名为"Book"的合约
contract Book { }

// 在同一个.sol文件下可以定义多个合约，且他们都使用同一个编译器版本
contract Student { }
```