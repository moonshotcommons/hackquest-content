# Content/概念

### Concept

现在让我们来学习另一个全局属性*block*，*block*属性下的全局变量都和区块信息有关。

在这一节中，我们首先学习block.number这个全局变量。

block.number是指当前的区块高度，也就是当前区块在整个区块链中的位置。每个新的区块都会递增这个值，所以它可以用来确定某个区块在区块链中的相对位置。

- 比喻
    
    *block.number*类似于产品的序列号，产品序列号用于唯一标识产品在生产中的顺序编号。每当一个新的区块被添加到区块链上时，它会被分配一个唯一的区块号（又称区块高度，每一个新产生的区块的区块号是递增的），就像产品在生产过程中被分配一个唯一的序列号。
    
- 真实用例
    
    在OpenZepplin的***[GovernorVotes](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/governance/extensions/GovernorVotes.sol#L25)***合约中，***clock***函数用于返回时间，如果`token.clock`发生异常，则会将当前的区块高度*block.number*作为返回值。
    
    ```solidity
    function clock() public view virtual override returns (uint48) {
        try token.clock() returns (uint48 timepoint) {
                return timepoint;
        } catch {
            return SafeCast.toUint48(block.number);
        }
    }
    ```
    

### Documentation

使用`block.number`来获取当前区块的高度。

```solidity
//通过block.number返回当前区块的高度，并赋值给了变量blockNumber。
uint256 blockNumber = block.number;
```

### FAQ

- 在测试的时候怎么修改block.number呢？
    

# Example/示例代码

```solidity
pragma solidity ^0.8.0;

contract BlockNumberExample {
    uint256 a = 0;

    //getCurrentBlockNumber的功能是返回当前区块的编号
    function getCurrentBlockNumber() public returns (uint256) {
        a = a + 1;
        return block.number;
    }
}
```
