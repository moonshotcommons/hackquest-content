# Content/概念

### Concept

到目前为止，我们已经学习了`library`，`interface`这两种特殊合约的定义，这一章中我们将学习最后一种特殊的合约定义方式——`abstract`，抽象合约。

抽象合约是一种不能被实例化的合约，只能被*继承*并作为其他合约的基类。它定义了一些函数和状态变量，并且实现了一些通用的功能。

- 比喻
    
    它类似于变装游戏中的基础人物，其他角色可以继承这个基类并添加特定的功能和外观。
    
- 真实用例
    
    在OpenZepplin给出的ERC20拓展合约***[ERC20Wrapper](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/token/ERC20/extensions/ERC20Wrapper.sol#L16C1-L86C2)***中，将***ERC20Wrapper***定义为了抽象合约，这样该合约将不能够被实例化。
    
    ```solidity
    abstract contract ERC20Wrapper is ERC20 {}
    ```
    

### Documentation

可以使用`abstract`关键字定义一个抽象合约。

```solidity
//这里我们定义了一个抽象合约ContractA
abstract contract ContractA { }
```

### FAQ

- 抽象合约和接口的区别？
    
    抽象合约和接口的最大区别在于，抽象合约可以包含*变量*和实现，而接口只包含没有实现的*函数*。
    
    ![Untitled](./img/1-1.png)
    
- 抽象合约和普通合约的区别？
    
    抽象合约和普通合约的唯一区别在于能否被*部署*。
    ```solidity
    abstractContract = MyAbstractContract(abstractAddress);  // error，抽象合约不能被部署
    regularContract = MyRegularContract(regularAddress);     // success
    ```
# Example/示例代码

```solidity
pragma solidity ^0.8.0;

// 抽象合约
abstract contract Animal {
    //抽象合约可以有变量的定义
    string public name;
    bool public hasEaten;

    event EatEvent(string name);
    //也可以有构造函数
    constructor(string memory _name) {
        name = _name;
    }
    
    function speak() public virtual returns (string memory);
    
    function eat() public virtual {
        // 抽象合约可以包含实现
        // 具体的逻辑可以在子合约中重写
        hasEaten = true;
    }
    
}

// 实现抽象合约的合约
contract Cat is Animal {
    constructor(string memory _name) Animal(_name) {}
    
    function speak() public override returns (string memory) {
        return "Meow";
    }
    
    function eat() public override {
        // 重写抽象合约中的 eat 函数
        // 提供猫的具体进食逻辑
        super.eat();
        emit EatEvent(name);
        // 进行其他猫的进食操作
    }
}
```