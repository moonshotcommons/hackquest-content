# Content/概念

### Concept

在前几节中，我们学习了字符串的定义与拼接。那么在本节中，我们将学习什么是字符串的长度并获取这个值。

一个 **字符串** 是由字符集合组成的，而 字符串长度 指的是它所包含的字符数。

- 比喻
    
    在word文档中，总有一个“总字数”的显示框。字符串的长度也就是字符串中存储字符的个数。
    
    例如，如果一个书信中有100个字符，那么它的长度就是100。同样地，在Solidity中，如果一个字符串中有10个字符，那么它的长度就是10。
    
- 真实用例
    
    在OpenZepplin的***Strings.sol***中，***[equal](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/utils/Strings.sol#L91)***函数使用了`bytes(a).length`语法获取了字符串***a***的长度。
    
    ```solidity
    function equal(string memory a, string memory b) internal pure returns (bool) {
        return bytes(a).length == bytes(b).length && keccak256(bytes(a)) == keccak256(bytes(b));
    }
    ```
    

### Documentation

要确定 Solidity 中字符串的**长度**，可以使用内置的 bytes 类型，该类型表示动态的bytes数组。bytes 类型有一个 length 属性，用来返回数组中的bytes数量。通过它我们可以得到字符串的长度。

```solidity
//值为 hello 的字符串变量
string hi = "hello";
//我们将字符串转换为 bytes，然后调用 length 函数获取长度
uint256 len = bytes(hi).length;
```

<aside>
💡 在 Solidity 中，字符串的长度通常使用 *uint256* 类型来表示。

</aside>

<aside>
💡 *bytes* 类型我们将在后续章节学习，这里我们简单了解即可。

</aside>

### FAQ

- 字符串长度一般何时会被使用？
    - 输入验证：我们有时需要验证输入以确保其符合某些要求。例如，我们可能要求字符串输入的长度不超过某个特定长度。为此我们需要获取输入的字符串长度。
    - 操作字符串：在操作字符串时，我们经常需要知道它们的长度，以执行连接和比较等操作。

# Example/示例代码

```solidity
pragma solidity ^0.8.0;

contract StringLength {
    string name = "the daughter";
    string testS;
    bytes testB;

	function test() public {
		testS = string.concat(name, "hello");
		uint l = bytes(testS).length;   //计算testS字符串长度，将其赋值给uint变量 l
		testB = bytes(testS);   //将字符串转化为byte数组
	}

  function getLength(string memory str) public pure returns(uint) {
      bytes memory bytesStr = bytes(str); //将字符串转化为byte数组
      return bytesStr.length; //返回字符串长度
  }
}
```
# Content/概念

### Concept

在本节中，我们将学习另一种类型，称为结构体。

在Solidity中，结构体是一种用户自定义的数据类型，其中可以包含多个不同类型的属性。

例如一个学生可以有很多属性，比如姓名、学号、年级等。我们可以将这些属性封装到一个结构体中。

![77406F69-4A0A-4DC4-A28B-8BC8E3E69FBB.jpeg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ac730351-c665-4bfd-8361-0501b9facd97/77406F69-4A0A-4DC4-A28B-8BC8E3E69FBB.jpeg)

- 比喻
    
    结构体可以存储很多信息，并且把他们有结构的存储起来。
    
    这就像你的简历，个人简介可以看作是一个数据结构，而个人优势又是另一个数据结构，但他们都是简历这个结构体的一员。
    
- 真实用例
    
    在OpenZepplin提供的***[AccessControl](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/access/AccessControl.sol#L50C1-L50C22)***合约中使用到了struct结构来表示一个管理员角色的信息，其中包括地址→是否有权限的映射和***adminRole***的哈希。
    
    ```solidity
    struct RoleData {
        mapping(address account => bool) hasRole;
        bytes32 adminRole;
    }
    ```
    

### Documentation

要定义一个结构体，首先你需要使用`struct`关键字，其后是结构体的名字。然后需要用`{}`将其属性括起来，`{}`里面每个属性用“`；`”隔开，结构体属性的定义与状态变量的定义相同，只是没有作用域这个概念。

```solidity
struct Cat {
  string name;
  address owner;
  uint256 age;
}
```

### FAQ

- 为什么使用结构体？
    
    结构体能更加方便的组织和管理相关的数据，使代码更加清晰和易于理解。
    
    例如我们可以创建多个"Student"结构体，每个结构体对应着一个特定的学生，并包含其所有属性，这能更好的组织和管理学生数据。