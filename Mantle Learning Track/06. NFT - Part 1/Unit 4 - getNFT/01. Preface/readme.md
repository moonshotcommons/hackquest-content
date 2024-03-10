# Content/Intro

In the previous section, we learned how to implement the functionality of **minting NFTs**, including deploying the *contract*.

After minting a new NFT, a natural step is to query the information of our newly minted NFT. Therefore, in this section, we will implement **a query function** that, given the TokenId, will find the information associated with the NFT and return it to the *function* caller.

In this section, we will learn how to:

1. Ensure the TokenId is valid.
2. Retrieve the specified NFT information.
3. *Return* the NFT information.

# Example/ Code

```solidity
pragma solidity ^0.8.17;

contract MyNFT {
  // Define a Token struct to store NFT information
  struct Token {
    string name; // NFT name
    string description; // NFT description
    address owner; // NFT owner address
  }

  // Use mapping to store the information of each NFT
  mapping(uint256 => Token) private tokens;

  // Record the next available NFT ID.
  uint256 nextTokenId = 1;

  // Create an NFT function to create a new NFT and assign it to the caller.
  function mint(string memory _name, string memory _description) public returns (uint256) {
    Token memory newNFT = Token(_name, _description, msg.sender);
    tokens[nextTokenId] = newNFT;

    nextTokenId++;

    return nextTokenId - 1;
  }
}
```
