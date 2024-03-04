# Content/概念

### Concept

在前面的课程中，我们学习了如何定义函数返回及如何使用return语句来将值作为*返回值*返回。

现在我们来进一步了解函数*返回值*的另一种形式——通过**已命名**的变量返回。

<aside>
💡 在这种模式下，我们无需使用return语句，只需直接为预先命名的返回值变量赋值即可。

</aside>

- 比喻
    
    我们预先确定了要返回的信息。无论黑匣子内部的处理如何，最终它都会将我们之前确定的那个信息作为返回值呈现给我们。
    
    通过这种方法，我们可以更加灵活地控制函数的返回值，使其根据预先设定的变量值来确定，而不再需要使用`return`语句来显式地返回值。
    
- 真实用例
    
    在Uniswap v2中的***[mint](https://github.com/Uniswap/v2-core/blob/ee547b17853e71ed4e0101ccfd52e70d5acded58/contracts/UniswapV2Pair.sol#L110)***函数，会将铸造所得的流动性***liquidity***作为返回值返回，这时这个返回值已经命名为***liquidity***，这样一来，函数里只需要对***liquidity***赋值，最后不需要`return`语句也会将该值返回给调用者。
    
    ```solidity
    function mint(address to) external lock returns (uint liquidity) {
        ...
        if (_totalSupply == 0) {
            liquidity = Math.sqrt(amount0.mul(amount1)).sub(MINIMUM_LIQUIDITY);
            _mint(address(0), MINIMUM_LIQUIDITY); // permanently lock the first MINIMUM_LIQUIDITY tokens
        } else {
            liquidity = Math.min(amount0.mul(_totalSupply) / _reserve0, amount1.mul(_totalSupply) / _reserve1);
        }
        require(liquidity > 0, 'UniswapV2: INSUFFICIENT_LIQUIDITY_MINTED');
        _mint(to, liquidity);
        ...
    }
    ```
    

### Documentation

要在**函数体**中返回一个值，我们可以使用关键字 `return`。

```solidity
function sum() public returns(int) {
	//这里我们使用关键字 return 返回整数5作为公共函数的输出
	return 5;
}

function name() returns(int res) {
		//如果没有对res赋值，则会返回res的默认值0
    //赋值后返回响应数据
    res= 5;
}
```

<aside>
💡 要在`函数头`中定义要返回的值，我们使用关键字 `returns`，但是要在 *函数体* 中返回值，则使用关键字 `return`。

</aside>

### FAQ

- 什么时候需要使用已经命名的返回值？
    
    当函数有具体的返回值目标时，使用已命名的返回值类型可以使代码更易懂。例如，如果一个函数的返回值声明为uint256 count，读者一看就知道该函数将返回一个计数值。这种明确的返回值命名有助于更好地理解函数的预期结果。

# Example/示例代码

```solidity
pragma solidity ^0.8.7;

contract Math {
    //我们定义了两个要返回的int值，k返回5，j将以默认值0返回,因为我们没有给它赋值
		function sum() public returns(int k, int j) {
        k = 5;
    }
}
```
