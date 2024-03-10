# Content/Minting the NFT

After associating TokenId with the kitty’s information, we can mint the NFT corresponding to the TokenId.

In this step, we will call the *function* ***_mint*** provided by ERC721. This function **accepts two parameters: the ***owner*** of the NFT and the ***TokenId***. 

We already have both of these parameters, corresponding to the *parameters* ***owner*** and the state variable ***_tokenIdCounter***.

**Syntax**

function call

- hint
    
    ```solidity
    _mint(owner, TokenId);
    ```
    
