# Content/Define nextTokenID

Finally, we keep talking about TokenIds, but how do we know how many tokens we’ve created and what’s the TokenId for the **next NFT**?

We should have a counter to represent the next available TokenId.

Every time we create a new NFT, we will use this counter to be the TokenId of the newly created NFT, and will increment this counter by one since that value has been used.  

We will use a uint256 to represent the TokenId because the id should never be negative, and this is the largest integer we could have. 

> This is also common practice in data structure: a struct to represent the object, a mapping to map from id to that object, and a counter to count how many objects in total, the same counter also indicate the id for next object. You will see this pattern in almost all resources managing projects: a collection of books, students, courses, etc.
> 

**Syntax**

value types

- hint
    
    ```solidity
    contract Example{
      uint256 TokenId;
    }
    ```