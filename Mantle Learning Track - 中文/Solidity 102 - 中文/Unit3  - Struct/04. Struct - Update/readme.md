# Content/概念

### Concept

到目前为止，我们已经讨论了结构体的定义，初始化和访问。

结构体通常在创建后需要修改其属性的值。这可能是因为需要更新数据、记录新的状态或者进行其他与结构体相关的操作。

因此，我们还需要知道如何修改结构体中的属性。

- 比喻
    
    学生有可能会长高，所以我们需要更新他的身高信息。
    
- 真实用例
    
    在OpenZepplin的***AccessControl***合约中，***[_setRoleAdmin()](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/access/AccessControl.sol#L172C1-L172C1)***函数从mapping中检索到***_roles[role]***结构体后，为该结构体的***adminRole***属性赋值。
    
    ```solidity
    struct RoleData {
        mapping(address account => bool) hasRole;
        bytes32 adminRole;
    }
    mapping(bytes32 role => RoleData) private _roles;
    
    function _setRoleAdmin(bytes32 role, bytes32 adminRole) internal virtual {
        _roles[role].adminRole = adminRole;
    }
    ```
    

### Documentation

想要修改结构体的属性，我们可以使用如下语法：

```solidity
student.name = "Thomas";
```

这里我们将***student***实例的***name***属性修改为了“*Thomas*”。

<aside>
💡 在结构体的属性修改时，要修改的值和属性的类型必须相同。

</aside>

### FAQ

- 结构体修改时需要注意什么？
    
    在结构体的属性修改时，要修改的值和属性的类型必须相同。
    
- 修改和定义的联系？
    
    我们在结构体的定义时讲过，结构体的属性类似于状态变量的定义。所以结构体属性的修改也和变量的修改很类似。只不过在变量的访问形式上有一定的区别。

# Example/示例代码

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Example {
  struct Student {
    string name;
    uint256 studentId;
    uint256 grade;
  }
  //我们在这个函数中先初始化了一个名为student的实例，其原名为Alice，然后我们将其name改为了Bob
  //并将旧名字和新名字作为返回值分别返回
  function testUpdate() public pure returns(string memory oldName, string memory newName) {
    Student memory student = Student("Alice", 1, 3);
    oldName = student.name;
    student.name = "Bob";
    newName = student.name;
  }
}
```