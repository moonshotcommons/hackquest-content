# Content/Content

### Concept

Now we will learn an alternative way to define and return outputs without explicitly using the return keyword in a function body.

- Metaphor
    
    We have **pre-determined** the information to be returned. Regardless of how the black box processes internally, in the end, it will present to us the information we had previously determined as the return value.
    
    Through this approach, we can have more flexible control over the function's return value, making it determined based on pre-set variable values, and eliminating the need for explicit **return** statements.
    
- Real Use Case
    
    In the Uniswap v2, the ***[mint***](https://github.com/Uniswap/v2-core/blob/ee547b17853e71ed4e0101ccfd52e70d5acded58/contracts/UniswapV2Pair.sol#L110) function returns the obtained ***liquidity*** as a return value. At this point, this return value is already named ***liquidity***, so within the function, you only need to assign a value to 'liquidity,' and there's no need for a **return** statement as it will automatically `return` this value to the caller.
    
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

```solidity
function sum() returns(int return_val){
    //We assign the return value to the return variable
    return_val = 5;
}
```

We define the variable to be returned in the header with its type and name, just like input parameters. Then we assign values to return variables. 

### FAQ

- Is there another way to return multiple things?
    
    Sometimes, we want to return multiple things, or we don’t want to explicitly write the return command. We could define *variables* in the return section in the *function header*, and assign values to them in function body. 
    
    ```solidity
    function sum(int a, int b) returns(int s, int ss,){
      //Here we assigned the value to variables defined in the header
      //and the function will return it eventually 
      s = a + b;
      ss = a+ s;
    }
    ```
    

# Example/Example

```solidity
pragma solidity ^0.8.7;
contract Math {
  //we defined two int to return, j will be returned in default value 0
  //since we didn't assign value to it
  function sum() public returns(int k, int j){
    k = 10;
  }
}
```
