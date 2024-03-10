# Content/Assigning Return Values

So far, we have completed the functionality of retrieving corresponding NFT information through TokenId.

Next, we will complete the final action of the query: assigning values to the *function* return value.

Since the *return* value of the *function* has been named when defining the *function*, we can directly assign values to the corresponding *return variable*.

**Syntax**

value types

- hint
    
    ```solidity
    name = token.name;
    description = token.description;
    owner = token.owner;
    ```