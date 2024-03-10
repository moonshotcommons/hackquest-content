# Content/更新 balances

在进行了权限控制后，我们就可以真正开始“**铸造**”了。

首先当然是更新***balances***映射中记录的代币余额，我们需要将代币的数量***amount***加到与***recipient***账户地址对应的余额中。

**Syntax Review**

mapping

- 提示
```slodity
//更新balances
balances[to] += amount;
```