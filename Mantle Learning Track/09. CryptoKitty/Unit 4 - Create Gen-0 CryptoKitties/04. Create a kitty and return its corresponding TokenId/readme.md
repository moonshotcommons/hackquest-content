# Content/Create a kitty and return its corresponding TokenId

In the previous step, we generated the genes for our kitty. Now, with this information, we can proceed to create the kitty using the ***_createKitty*** function.

> To recap, the parameter structure of this *function* is as follows: mom's TokenId, dad's TokenId, generation, genes, and owner of the cat.
> 

For the first generation, we'll assume the kitty doesn't have any parents. Therefore, we'll set both ***momId*** and ***dadId*** to *0*. The ***generation*** will also be set to *0*. The ***genes*** will be the random number we've previously generated, and the ***owner*** will be the function's caller.

Lastly, the ***createKittyGen0*** *function* should return the TokenId of the newly created kitty. To achieve this, we'll simply return the result of the ***_createKitty*** function call, which both creates the kitty and provides the next available Token ID.

**Syntax**

function call

- hint
    
    ```solidity
    return create(0, 0, 0, gene, owner);
    ```
    
