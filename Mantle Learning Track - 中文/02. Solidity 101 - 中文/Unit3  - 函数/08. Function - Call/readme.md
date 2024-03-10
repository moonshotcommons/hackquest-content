# Content/概念

### Concept

现在我们已经学习了如何定义函数，现在是时候学习如何实际访问（调用）函数了。

- 比喻
    
    调用函数就像按下黑盒子上的按钮，它将为您执行某些操作。在你调用该函数之前，什么都不会发生。
    
    当程序执行到调用函数的语句时，会跳转到该函数所在的位置开始执行函数内部的代码，并且可以通过传递参数给函数来影响函数的行为。当函数执行完毕后，会返回到调用它的语句处继续执行后面的代码。
    
- 真实用例
    
    在ERC20合约的***[transferFrom](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/8186c07a83c09046c6fbaa90a035ee47e4d7d785/contracts/token/ERC20/ERC20.sol#L163-L168)***函数中先后调用了***_spendAllowance***和***_transfer***以完成授权的更新和转账的功能。
    
    ```solidity
    	function transferFrom(address from, address to, uint256 value) public virtual returns (bool) {
          address spender = _msgSender();
          _spendAllowance(from, spender, value);
          _transfer(from, to, value);
          return true;
      }
    ```
    

### Documentation

*调用函数*需要知道函数的名称以及可能需要传递给它的参数。

```solidity
//add 是一个返回两个整数之和的函数
//我们调用了 add 函数并将数字 2 和 3 作为参数传递给它。
//最后，该函数返回了一个int结果并存储在变量 d 中。
int d = add(2, 3);

//addMul函数返回两个值
//1. a和b的和
//2. a和b的乘积
(int d,int e) = addMul(a, b);
```

### FAQ

- 调用函数前后的代码是怎么执行的？
    
    ```solidity
    function b() public {
    		//代码片段3
    }
    function a() public {
    		//代码片段1
    		b();
    		//代码片段2
    }
    ```
    
    ![Untitled](./img/8-1.png.png)

# Example/示例代码

```solidity
pragma solidity 0.8.4;

contract A {
		// 定义一个名为 add 的公共函数，接收两个整型参数 a 和 b，并返回它们的和
    function add(int a, int b) public returns(int) {
				return a + b;
    }
		// 定义一个名为 addUp 的公共函数，接收三个整型参数 a、b 和 c，并返回它们的和
    function addUp(int a, int b, int c) public returns(int) {
        // 调用 add 函数将 a 和 b 相加，将结果保存在变量 d 中
        int d = add(a, b);
				// 调用 add 函数将 d 和 c 相加，将结果作为 addUp 函数的返回值返回
        return add(d, c);
    }

    // 定义一个名为 addMul 的公共函数，接收两个整型参数 a 和 b，并返回它们的和与积
    function addMul(int a, int b) public returns(int, int) {
				return (a + b, a * b);
    }
		// 定义一个名为 addMulUp 的公共函数，接收三个整型参数 a、b 和 c，返回两个整数类型的值，分别为a+b+c, (a+b)*c
    function addMulUp(int a, int b, int c) public returns(int, int) {
        (int d,int e) = addMul(a, b);
        return addMul(d, c);
    }
}
```
