# Content/Intro

We have completed the ***deleteById** function* to remove an NFT with a given Id from the user’s wallet.

Now, we can start to write the **transaction function**, namely ***transfer***.

The ***transfer** function* allows users to send NFTs to other *addresses*, facilitating the circulation of digital asset value.

To implement this *function*, in this section, we need to:

1. define the ***transfer** function*.
2. check if the recipient address and tokenId are valid.
3. query the information of the NFT to be transferred based on its tokenId.
4. restrict the caller to be the owner of the NFT**.**

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

  // Get all NFT IDs owned by a specified address

  function getTokensByOwner(address _owner) public view returns (uint256[] memory) {
    return ownerTokens[_owner];
  }

  function deleteById(address account, uint256 _tokenId) internal {
    uint256[] storage ownerTokenList = ownerTokens[account];

    for (uint256 i = 0; i < ownerTokenList.length; i++) {
      if (ownerTokenList[i] == _tokenId) {
        // Swap the NFT ID with the last element of the array, then delete the last element of the array.
        ownerTokenList[i] = ownerTokenList[ownerTokenList.length - 1];
        ownerTokenList.pop();
        break;
      }
    }
  }
}
```