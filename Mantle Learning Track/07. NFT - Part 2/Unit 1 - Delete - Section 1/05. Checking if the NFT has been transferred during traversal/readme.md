# Content/Checking if the NFT has been transferred during traversal

Now let's enter the *for loop*. In each iteration, we need to check if the TokenId is the same as the TokenId specified by the input *parameter **_tokenId***.

If the TokenId matches the one we are looking for, we will execute the deletion logic. Otherwise, we will continue with the traversal.

Based on the above description, we need a **control flow** statement, and the most suitable control flow for "if...then..." is the `if` statement.

**Syntax Review**

if, array

- hint
    
    ```solidity
    if (arr[i] == TokenId) { }
    ```
    
