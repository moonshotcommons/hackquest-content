# Content/Define the kitties’ mapping

In the previous step, we mentioned that we need to establish a one-to-one relationship between the kitty information and the TokenId.

> At this moment, we need to retrieve the kitty’s information using its ID, but we don't need to find the ID using the kitty's information.
> 

To achieve this one-to-one relationship, we can use a mapping. In this case, we need a *mapping* from uint256 to ***Kitty***.

In terms of visibility, we choose public to facilitate querying.

**Syntax**

mapping

- hint
    
    ```solidity
    mapping(uint256 => Kitty) public kitties;
    ```
    
