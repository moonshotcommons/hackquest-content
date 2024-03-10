# Content/概念

### Concept

在我们讨论了如何定义结构体之后，我们需要知道该怎么初始化一个结构体。

初始化结构体意味着创建一个新的结构体实例，我们可以通过指定数据来创建一个独特的结构体。

- 比喻
    
    假设我们有一个结构体称为"学生"，它有几个属性，比如姓名、学号和年级。结构体定义了学生的属性，但是我们需要具体的学生实例来代表一个具体的学生。
    
    初始化结构体就像是招收一位新学生。当我们初始化结构体时，我们为每个属性赋予具体的值，就像是为学生指定姓名、学号和年级。通过为每个属性赋值，我们创建了一个特定的学生实例。
    
- 真实用例
    
    在***GovernorStorage***合约中，通过结构体名( `{param name : param}` )的方式初始化[***ProposalDetails***](https://github.com/OpenZeppelin/openzeppelin-contracts-upgradeable/blob/7d7ad99dee371e0ee042e2999aaf43941dea1513/contracts/governance/extensions/GovernorStorageUpgradeable.sol#L46C1-L46C1)结构体。
    
    ```solidity
    struct ProposalDetails {
        address[] targets;
        uint256[] values;
        bytes[] calldatas;
        bytes32 descriptionHash;
    }
    _proposalDetails[proposalId] = ProposalDetails({
        targets: targets,
        values: values,
        calldatas: calldatas,
        descriptionHash: keccak256(bytes(description))
    });
    ```
    

### Documentation

要想初始化一个结构体，需要使用结构体的名字后跟括号的方式，括号里面是结构体的属性值，这需要和结构体定义时的属性一一对应。

```solidity
Student("zhangsan", 18);
```

### FAQ

- 在结构体初始化的时候有什么需要注意的吗？
    
    结构体只能够存储在像*mapping*，*array*这样的引用类型当中，因此我们还可以通过在这样的引用类型中检索到空结构体后再对其进行赋值。
    
    这也是一种初始化的方式。

# Example/示例代码

```solidity
pragma solidity ^0.8.0;

contract Example {
  struct Student {
    string name;
    uint256 studentId;
    uint256 grade;
  }
  //我们在这个函数中初始化了一个Alice学生示例，并将其作为函数的返回值返回
  function testDefinition() public pure returns(Student memory) {
    Student memory student = Student("Alice", 1, 3);
    return student;
  }
}
```