# Content/Exit the Loop

So far, we have finished the deletion process inside the `if` statement, but this statement is not completed yet.

We still need a statement to **exit the loop**.

> Because we have already achieved the purpose of traversal after finding the TokenId to be deleted, there is no need to continue the traversal! This would waste resources.
> 

Therefore, we use the `break` statement to exit the loop.

**Syntax Review**

break

- hint
    
    ```solidity
    for(uint i = 0; i < 10; i++) {
      break;
    }
    ```
    