# Content/Intro

We have successfully minted the NFT, and now we need to increment the ***nextTokenId*** to prepare for the creation of the next NFT.

Then, return the TokenId of the newly created NFT. This provides the caller with the TokenId for further reference or use.

So far, we’ve finished our ***mint*** *function* and we could go to try it out! 

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
  function mint(string memory _name, string memory _description)
    public
    returns (uint256)
  {
    Token memory newNFT = Token(_name, _description, msg.sender);
    tokens[nextTokenId] = newNFT;
 
  }
}

```