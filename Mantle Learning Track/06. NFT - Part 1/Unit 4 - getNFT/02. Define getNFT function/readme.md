# Content/Define getNFT function

First, we need to clarify the *function's* purpose. As we mentioned earlier, the *function* is used to **query information** about an NFT, so it's natural that we need an input *parameter *****_***tokenId*** to specify the TokenId of the NFT to be queried.

The query *function* should not modify the *contract's state* *variables*, so the *function* should have `view` as *state mutability*.

In terms of *function visibility*, we choose to use `public` because we want the *function* to be accessible for querying NFT information regardless of whether it's inside or outside the *contract*.

As a query *function*, the most important thing is to define the return value. For demonstration purposes, we choose to return the NFT's **name, description,** and **owner** one by one.

For ***name*** and ***description***, they’re in type string. Since string type *variables* must specify the *data location* when used as local *variables*, we define them as `string memory`.

**Syntax**

function parameters, return, calling, string, data location

- hint
    
    ```solidity
    //A function named getNFT
    function getNFT(uint256 _Id) public view returns (string memory name, string memory description, address owner);
    ```
    
