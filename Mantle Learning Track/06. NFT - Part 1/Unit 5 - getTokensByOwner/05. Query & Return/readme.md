# Content/Query & Return

We defined the *function header*, and now we will proceed to implement the function body, and we will complete the query and return functionality in one line.

First, we need to find the corresponding wallet in the ***ownerTokens*** based on the input *parameter **_owner***.

After obtaining the corresponding wallet, we directly use the `return` statement to *return* it.

**Syntax Review**

function parameters, return, calling

- hint
    
    ```solidity
    //Let's use the return value of a function
    //A function named "add" that takes two input parameters and returns the sum as an unsigned integer (uint)
    function add(uint num1, uint num2) public pure returns(uint){
      return num1+num2;
    }
    ```
    