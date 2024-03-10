# Content/Define the breed function

First, let’s define the ***breed*** function. 

The primary objective of this function is to **breed** a new generation of kitties based on the specified mother and father. The genes of the offspring will be determined by its parents.

To achieve this, we require two input parameters of type `uint256`, representing the TokenIds of the mother and father kitties.

The function will also return a value, which is the TokenId of the newly bred kitty.

Regarding the function's visibility, we'll set it to `public` to ensure it's callable both internally and externally within the contract."

**Syntax**

function

scope

- hint
    
    ```solidity
    function breed(uint256 momId, uint256 dadId) public returns (uint256) { }
    ```
    
