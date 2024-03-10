# Content/返回对应地址的余额

在完成函数的定义之后，我们在这一步中实现函数的功能。

首先，为了返回指定地址对应的余额，我们要从***balances***映射中查找与***account***地址对应的余额。

在查询到余额后，需要使用`return`语句将该值作为返回值返回。

**Syntax**

return mapping

- 提示
```solidity
//例如在这里，我们定义了一个函数可以返回整型“5”
function getData() public view returns(uint256){
    return 5;
}
```