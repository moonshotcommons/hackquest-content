# Content/Create new kitties

After calculating the kitty's gene and generation number, we have all the necessary information to generate a new kitty. Specifically:

1. Kitty Dad's TokenId - ***dadId***
2. Kitty Mom's TokenId - ***momId***
3. Genes - ***newGenes***
4. Generation - ***newGeneration***
5. Kitty owner - *msg.sender*

Do you remember the ***_createKitty*** function we wrote? It will come in handy here. All we need to do is pass the above information as parameters and call the ***_createKitty*** *function*.

**Syntax**

function call

- hint
    
    ```solidity
    create(someMessage);
    ```
    
