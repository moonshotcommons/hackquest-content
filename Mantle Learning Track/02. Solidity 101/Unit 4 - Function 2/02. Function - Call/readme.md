# Content/Content

### Concept

Function call refers to the act of invoking a specific *function* within a *contract*, triggering the execution of its code and potentially modifying the *contract's state* or returning a value.

- Metaphor
    
    The calling step is like pushing the button on the **black box** and it’ll do something for you. Nothing will happen until you call the function.
    
- Real Use Case
    
    In the ***[transferFrom](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/8186c07a83c09046c6fbaa90a035ee47e4d7d785/contracts/token/ERC20/ERC20.sol#L163-L168)*** function of the ERC20 contract, the ***_spendAllowance*** and ***_transfer*** functions are called sequentially to complete the functionality of updating authorization and transferring funds.
    
    ```solidity
    	function transferFrom(address from, address to, uint256 value) public virtual returns (bool) {
          address spender = _msgSender();
          _spendAllowance(from, spender, value);
          _transfer(from, to, value);
          return true;
      }
    ```
    

### Documentation

```solidity
//let add be the function that returns the sum of two int 
int d = add(a, b);
```

To call a function, we use its name with inputs.

### FAQ

- How to receive multiple returns from a function call?
    
    In the previous lessons, we’ve seen that functions could have **multiple** return values, then it’s a question of how to call the *function* with **multiple** return values and catch all these return values. 
    
    ```solidity
    //assume add Mul returns two things
    //1. the sum of a, b 
    //2. the product of a, b
    (int d, int e) = addMul(a, b);
    ```
    

# Example/Example

```solidity
contract A {

  function add(int a, int b) public returns(int){
    return a + b;
  }

  function addUp(int a, int b, int c) public returns(int){
    int d = add(a, b);
    return add(d, c);
  }

  function addMul(int a, int b) public returns(int, int){
    return (a + b, a * b);
  }

  function addMulUp(int a, int b, int c) public returns(int, int){
    (int d, int e) = addMul(a, b);
    return addMul(d, c + e);
  }
}
```
