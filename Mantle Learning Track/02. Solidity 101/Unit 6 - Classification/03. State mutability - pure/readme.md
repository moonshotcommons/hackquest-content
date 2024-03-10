# Content/Content

### Concept

A pure *function* in Solidity is a function that doesn't modify the *contract's states*, access external *contracts*, or read the *state* of the blockchain; it only performs computations on its input *parameters* and returns a computed result.

- Metaphor
    
    Think of this function as a black box that’s not connected to the internet. *Pure functions* don’t need any information other than input *parameters*. You could copy and paste the *function* to any other *contract*, in any location, and with the same input, it will always output the same result. 
    
    A *pure function* doesn’t use any *state variables*, or call any other *functions*. Everything it needs is inside the *function*. 
    
- Real Use Case
    
    ```solidity
    function tryAdd(uint256 a, uint256 b) internal pure returns (bool, uint256) {
        unchecked {
            uint256 c = a + b;
            if (c < a) return (false, 0);
            return (true, c);
        }
    }
    ```
    
    In the Math *contract*, this ***[tryAdd***](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/utils/math/Math.sol#L25-L31) *function* that returns the addition of two *unsigned integers* is a *pure function*. It performs computations based solely on its inputs and doesn't interact with the contract's state or external data.
    

### Documentation

```solidity
function add() public pure {
  //function body 
}
```

To define a *function* to be pure, we use the keyword `pure` in the function header.

<aside>
💡 For consistency, we will always follow this order: *function name* and *parameters*, *scope*, *state mutability*, and *return*.

</aside>

### FAQ

- Why use Pure functions?
    
    In the previous sections, we learned that state variables persist permanently on the blockchain. As a result, modifying *state variables* requires paying *gas fees.* 
    
    Pure and *view functions* (which we will learn in the next lesson) do not alter the on-chain state, so users can invoke them directly without paying any gas fees.
    
    It's part of an agreement between the developer and the Ethereum network, where the developer promises that the function won't interact with the state in certain ways, and in return, the *function calls* can be optimized and used freely in certain contexts.
    
- When to mark the function as view?
    
    An easy way is that your IDE, like Remix, will remind you of your function state mutability, so if you’re not sure, follow Remix’s warning, a little yellow exclamation mark. 
    

# Example/Example

```solidity
pragma solidity ^0.8.0;
contract Example {
  mapping(int => int) aa;
  //this is a pure function
  function add(int a, int b) public pure returns(int) {
    return a + b;
  }
  //this is not 
  function addNotPure(int a, int b) public returns(int) {
    aa[0] = a + b;
    return aa[0];
  }
}
```
