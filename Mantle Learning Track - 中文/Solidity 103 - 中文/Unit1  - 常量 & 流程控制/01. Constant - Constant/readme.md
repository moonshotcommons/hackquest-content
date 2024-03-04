# Content/概念

### Concept

在前面我们已经学了很多变量的定义方式，例如*storage*和*memory*可以定义变量的存储位置，*public*和*private*可以定义变量的可见性。

在这一节中，我们将学习一种特殊的变量定义方式：`constant`。

`constant`是一种用于定义常量的关键字。常量是在程序执行期间不会发生变化的值。它们在声明后被固定，并且无法在运行时被修改。

- 比喻
    
    例如，物理学中的光速被认为是一个常量（299,792,458 米/秒）：
    
    ![E757A8CF-1164-4D1D-AA38-C6D317B49ADD.jpeg](./img/1-1.jpeg)
    
- 真实用例
    
    例如OpenZepplin中的[***AccessControl**](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/access/AccessControl.sol#L57C1-L57C55)合约*，将变量***DEFAULT_ADMIN_ROLE***设为*0x00*。
    
    ***AccessControl***是一个权限控制合约，合约中用`bytes32` 来表示不同用户的角色。合约默认管理者的角色是0。
    
    ```solidity
    bytes32 public constant DEFAULT_ADMIN_ROLE = 0x00;
    ```
    

### Documentation

要定义constant变量，我们需要在变量类型和变量名中间使用关键字`constant`。constant变量通常使用大写字母表示

```solidity
//将1赋值给了常量NUM。
uint256 constant NUM = 1;
```

<aside>
💡 `constant`只能用于*状态变量*的定义。因为`constant`修饰的变量将会*硬编码*到*字节码*中，而字节码是在合约部署时就生成的值，所以不可能在函数运行时再改变字节码。

</aside>

### FAQ

- 为什么使用constant？
    
    constant申明的变量不会被写入合约的*storage*中，而是直接在编译时被硬编码到字节码中。
    
    这样做的好处是，由于这些常量的值是在字节码中的，所以我们不需要读取存储空间来获取值，从而节省了*gas*消耗。

# Example/示例代码

```solidity
pragma solidity ^0.8.0;

contract Example {
  //在这里定义了一个常量MAXINPUT，其值不可以在合约中更改。
  uint256 constant public MAXINPUT = 1;

  function input(uint256 num) public {
    require(num < MAXINPUT);
  }
}
```
