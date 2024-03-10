# Content/Traverse Wallet

Now, let’s traverse all the TokenIds in this wallet, as we need to compare them one by one with our input  ***_tokenId***.

The traversal process is actually equivalent to taking out each element of the array individually from the first element to the last element for comparison.

In this process, we need to define an **index** to indicate the current position we are accessing in the *array* and increase this index after accessing it.

To implement this process, we need to use a for loop because a *for* *loop* is actually a process of index incrementation.

**Syntax Review**

for

- hint
    
    ```solidity
    for (uint256 i = 0; i < TokenArray.length; i++) {}
    ```
    
