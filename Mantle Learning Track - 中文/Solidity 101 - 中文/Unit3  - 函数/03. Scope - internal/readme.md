# Content/概念

在知道如何定义函数后，我们还需要定义一个可见性，也称为作用域。它指定了我们何时可以访问此 变量 或 函数。

- 比喻
    
    就像你的信息一样，私密的信息你不会公开，所以定义为private。而可以公开的需要被大众知晓的信息定义为public。
    
- 真实用例
    
    在ERC20中有像***[transfer](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/8186c07a83c09046c6fbaa90a035ee47e4d7d785/contracts/token/ERC20/ERC20.sol#L118)***这样的`public`函数，需要提供给所有的人调用，以触发转账操作。
    
    ```solidity
    function transfer(address to, uint256 value) public virtual returns (bool) {
        address owner = _msgSender();
        _transfer(owner, to, value);
        return true;
    }
    ```
    
    但也有像[_balances](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/8186c07a83c09046c6fbaa90a035ee47e4d7d785/contracts/token/ERC20/ERC20.sol#L39C59-L39C59)一样的`private` 变量， 它不需要提供给外人，即使我们可以使用权限控制来保护余额信息不被泄露。
    
    ```solidity
    mapping(address account => uint256) private _balances;
    ```
    

### Documentation

要定义一个 *公共变量* 或 *公共函数*，我们使用关键字 `public`，并将其放在 *变量* 名称之前或 *函数* 参数之后。

```solidity
uint public a;
function aa() public { 
	//funciton body 
}
```

### FAQ

- 为什么需要区分public和private？
    1. **安全性**：通过将某些函数标记为private，可以确保只有合约内部的其他函数可以调用它们。这可以防止外部恶意合约或攻击者调用可能对合约安全性构成威胁的内部函数。
    2. **隐私性**：有时，合约可能包含处理敏感信息的函数。通过将这些函数标记为private，可以防止外部查看或访问这些敏感数据。这有助于保护用户的隐私。
    3. **优化和成本**：public函数通常需要更多的燃气（gas）来执行，因为它们需要处理许多安全性和访问控制检查。通过将某些非必要公开函数标记为private，可以减少合约执行时的燃气成本，从而提高效率。

# Example/示例代码

```solidity
contract A {
  //***aa*** 和 ***bb*** 函数，以及 ***a*** 变量可以从任何地方访问，因为它们是 public 。
	//***b*** 和 ***bbb***只能从合约内部访问，因为它们是 private 。
	uint public a;
	uint private b;
	function aa() public {
		//这与a = a + 1 等同;
		a++;
	}
	function bb() public {
		b++;
	}
  function bbb() private {
    b++;
  }
}
```
