# Content/更新收款者的余额

由于在上一步中我们只更新了转账者的余额，所以我们还需要更新收款者的余额。

逻辑是相反的，需要给收款者的余额加上转账金额。

**Syntax Review**

variable

- 提示
```solidity
//更新balances
balances[to] += amount;
```