# Content/概念

### Concept

我们接下来会学习 abi 编码在函数调用时的作用，在开始之前，你需要先了解什么是函数签名。

函数签名是一个函数的唯一标识符，它由*函数名*和*参数类型*组成。在 Solidity 中，所有函数调用都通过*函数签名*作为唯一标识。

- 比喻
    
    例如，学校里有很多学生，叫 *Harry* 的有四个，身高*165*的有*10*个，*红色头发*的有*15*个，那我们称呼学生能确保唯一性呢？我们把能定义这个小朋友的所有信息：“*Harry，165，红色头发*”都描述一遍。
    
    这就像函数签名，我们把这个函数的名字，和所有接收的参数都描述一遍。
    
- 真实用例
    
    在 [***IERC1155Receiver***](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/token/ERC1155/IERC1155Receiver.sol#L18)中，我们规定***onERC1155Received*** 函数必须返回自己函数签名的哈希前四位，才能表示调用成功（函数签名的哈希前四位则是函数选择器）
    
    ```solidity
    /**
     * @dev Handles the receipt of a single ERC1155 token type. This function is
     * called at the end of a `safeTransferFrom` after the balance has been updated.
     *
     * NOTE: To accept the transfer, this must return
     * `bytes4(keccak256("onERC1155Received(address,address,uint256,uint256,bytes)"))`
     * (i.e. 0xf23a6e61, or its own function selector).
     *
     * @param operator The address which initiated the transfer (i.e. msg.sender)
     * @param from The address which previously owned the token
     * @param id The ID of the token being transferred
     * @param value The amount of tokens being transferred
     * @param data Additional data with no specified format
     * @return `bytes4(keccak256("onERC1155Received(address,address,uint256,uint256,bytes)"))` if transfer is allowed
     */
    function onERC1155Received(
        address operator,
        address from,
        uint256 id,
        uint256 value,
        bytes calldata data
    ) external returns (bytes4);
    ```
    

### Documentation

函数签名是*函数名*+*参数字段类型*的字符串。没有空格，不用缩写。

```solidity
function hello(uint256 a, address b, bool c) {...}
signature = "hello(uint256,address,bool)"；
```

### FAQ

- 两个不同的函数的函数签名可能相同吗？
    
    在同一个合约里不可能，Solidity不允许同一个合约里面有两个函数有相同的函数签名因为Solidity通过函数签名的哈希值前四位定位需要调用的函数，如果函数签名一样，那哈希值前四位也会一样，这样的话没有办法确定到底调用哪个。
    
    在不同的合约里则可能。只要函数名，参数类型和顺序一致就OK。
    

# Example/示例代码

```solidity
pragma solidity ^0.8.0;

contract FunctionSignature {
  function dosome(uint256 num, string memory text) public pure returns (string memory signature) {
    // 计算函数签名
    signature = "dosome(uint256,string)";
  }
}
```
