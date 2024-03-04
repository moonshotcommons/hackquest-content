# Content/概念

### Concept

刚刚我们学习了函数签名，现在让我们看看*函数签名*真正的用途：函数选择器。
函数选择器是*函数签名*的哈希前四个字节，用于在编码后的数据中唯一标识函数。

<aside>
💡 在 Solidity 中，所有函数调用其实是通过函数选择器作为唯一标识。

</aside>

- 比喻
    
    想象一下，每个学生都有一个详细的档案，其中包含了他们的所有信息，如***姓名***、***出生日期***、***家庭住址***、***兴趣爱好***等。这个档案就像函数签名，它是学生的完整描述。
    
    但是，当老师需要快速识别一个学生时，查阅整个档案可能会浪费太多时间。因此，学校为每个学生提供了一个学生证，上面只有学生的照片和一个独特的学号。这个学号是从学生的档案中提取的关键信息，并进行了简化处理，使其成为一个短而独特的标识符。
    
    这个学号就像函数选择器。它是从*函数签名*（即学生的完整档案）中提取的，但只有前4个字节（即学号的长度）。尽管它比完整的档案简短得多，但它仍然是唯一的，可以用来快速识别学生（或函数）。
    
    当老师看到学生证上的学号时，他们可以迅速知道这是哪个学生，而不需要查看整个档案。同样，当智能合约需要调用一个函数时，它可以通过函数选择器迅速找到正确的函数，而不需要查看整个函数签名。
    
- 真实用例
    
    最经典的就是ERC721有一个回调函数 ***[onERC721Received](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/token/ERC721/utils/ERC721Holder.sol#L21C1-L21C47)***，该函数默认返回***onERC721Received*** 这个函数的函数选择器，我们可以直接使用*合约名.函数名.selector*的方式来获取函数选择器。
    
    ```solidity
    function onERC721Received(address, address, uint256, bytes memory) public virtual returns (bytes4) {
        return this.onERC721Received.selector;
    }
    ```
    

### Documentation

函数选择器是函数签名的哈希前*4*个字节。在这里我们直接取函数签名的前*4*个字节即可，或者也可以直接使用`functionName.selector`

```solidity
bytes4 selector = bytes4(keccak256(signature));
bytes4 selector = myFunction.selector;
```

### FAQ

- 那么为什么要使用函数选择器而不直接使用函数签名呢
    
    函数选择器只需要四个字节，大大节省了存储空间，这样会使链上的部署和调用都更加省gas。
    
- 选择器碰撞是什么？
    
    选择器碰撞是指两个不同的函数他们的函数选择器是一样的。
    
    例如`transferFrom(address,address,uint256)`的函数签名哈希为：
    
    *0x23b872dd7302113369cda2901243429419bec145408fa8b352b3dd92b66c680b*
    
    而`gasprice_bit_ether(int128)`的函数签名哈希为：
    
    *0x23b872ddd9b96c46b307d87a34b44cc03080be64e7bd1bf7c26e93b854ffbc75*
    
    他们的函数签名哈希其实是不同的，但是却有着相同的选择器：*0x23b872dd*
    
    <aside>
    💡 这样的两个函数在同一合约中是无法编译的，但是如果出现在代理合约和实现合约两个不同的合约中，就可能造成安全隐患。
    
    </aside>
    

# Example/示例代码

```solidity
pragma solidity ^0.8.0;

contract FunctionSignature {
  function dosome(uint256 num, string memory text) public pure returns (bytes4 selector1, bytes4 selector) {
    selector = bytes4(keccak256("dosome(uint256,string)"));
    selector1 = this.dosome.selector;
  }
}
```