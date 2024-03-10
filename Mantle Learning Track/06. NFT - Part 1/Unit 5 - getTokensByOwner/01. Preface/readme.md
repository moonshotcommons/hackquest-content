# Content/Intro

In the previous section, we learned how to query information about an NFT through its tokenId.

In an NFT system, it is also common to have the need to query all the NFTs owned by a particular address. Therefore, in this section, we will implement a query *function* that retrieves **all the NFTs** **owned by a** **given address**. To implement this functionality, we need to do the following steps:

1. Create a new mapping from address to the array of NFTs owned by that *address*. You should think of this *array* as a wallet, which tracks all your NFTs
2. Update the ***mint*** *function* so we also update our wallets correctly when minting a new NFT.
3. Retrieve the *array* of NFTs owned by the *address*.
4. Return this *array* as the result of the query.

At this point, the query is considered complete. By the end of this section, we can use Remix to query all the NFTs owned by a specified account address.

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

  // Use mapping to store the list of NFT IDs owned by each address
  mapping(address => uint256[]) private ownerTokens;

  // Record the next available NFT ID.
  uint256 nextTokenId = 1;

  // Create an NFT function to create a new NFT and assign it to the caller.
  function mint(string memory _name, string memory _description) public returns (uint256) {
    Token memory newNFT = Token(_name, _description, msg.sender);
    tokens[nextTokenId] = newNFT;
    ownerTokens[msg.sender].push(nextTokenId);
    nextTokenId++;
    return nextTokenId - 1;
  }

  //Create a function to get information on a specified NFT
 function getNFT(uint256 _tokenId) public view returns (string memory name, string memory description, address owner) {
    require(_tokenId >= 1 && _tokenId < nextTokenId, "Invalid token ID");
    Token memory token = tokens[_tokenId];
    name = token.name;
    description = token.description;
    owner = token.owner;
  }
}
```