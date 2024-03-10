# Content/Intro

In the previous section, we have created the *contract* and defined the core *variables*.

Now, let's add some functionality to the *contract*.

First, we need to define the ***mint** function*. The purpose of this function is to **create an NFT** defined by the caller of this *function* and add it to our system. 

In this section, we will

1. define the *function*.
2. create a new NFT within the ***Token***.
3. associate the new NFT with tokenId.

# Example/ Code

```solidity
pragma solidity ^0.8.17;

contract MyNFT {
  //Define a Token struct to store NFT information
  struct Token {
    string name; // NFT name
    string description; // NFT description
    address owner; // NFT owner address
  }

  // Use mapping to store the information of each NFT
  mapping(uint256 => Token) private tokens;

  // Keep track of the next available NFT ID.
  uint256 nextTokenId = 1;
 
}
```