# Content/Define owner mapping

The functionality we want to achieve in this section is to query all the NFTs owned by a specified *address*. It is obvious that we cannot achieve this with our current two *variables*, the ***Token***, and the ***tokens***.

We need a *variable* similar to a wallet, which links the address with all the **NFTs** it owns.

This is a mapping relationship, a *mapping* from an address to an array of TokenIds, representing all the NFTs owned by the *address*.

To better understand this *variable*, you can imagine it as a *mapping* from an **address** to a **wallet**, and the data structure of the wallet is an *array of TokenIds*.

> In the following tutorials, we will use the term wallet repeatedly to refer to an *array of TokenIds*.
> 

Therefore, we first need to define a `mapping`.

**Syntax**

mapping, array, address

- hint
    
    ```solidity
    contract Example{
      //For example, NFTs here can record the array of tokenIds of NFTs held by each address.
      mapping (address => uint256[]) private NFTs;
    }
    ```
    
