# Content/Define TokenID Mapping

Now we have a data structure to store all the information about one NFT.

Next step, since we will for sure have more than one NFT regulated by this *contract*, we should probably number all the **NFTs**, and somehow associate the number with each of our NFT. 

In other words, we will assign a **TokenId** to each NFT to be its unique number. 

A mapping is a natural choice because *mapping* adds relationships between two types of data. In our case: the uint and Token structure we just defined. 

> It’s a common practice in programming that when you have more than 1 objects in the same category, you can number them so it’s easier to **create**, **look up**, **update**, and even **delete** this object.
> 

**Syntax**

value types,mapping

- hint
    
    ```solidity
    contract Example{
      //For example, the apples variable can record detailed information for each appleId.
      mapping (uint256 => Apple) private apples;
    }
    ```