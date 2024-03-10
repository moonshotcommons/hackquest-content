# Content/Define the _createKitty function

Now, let’s define the ***_createKitty*** function. 

The main purpose of this *function* is to create an NFT (Kitty) based on the provided Kitty attributes.

Wait a second, do we want everyone to be able to create kitties freely? 

Not really, Kitties should be bred, so the  ***_createKitty*** *function* should only be for `internal` use within the contract, thus we define its visibility as `private`.

We also need a return the next available Token ID to the caller so they can check the newly created kitty.

**Syntax**

function

scope

return

- hint
    
    ```solidity
    //For example, here we pass the genes and owner information to the create function, and it has a return value of type uint256.
    function create(uint256 genes, address owner) private returns (uint256) { }
    ```
    
