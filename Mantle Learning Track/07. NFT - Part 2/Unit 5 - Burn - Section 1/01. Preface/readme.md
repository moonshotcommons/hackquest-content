# Content/Intro

So far, we have completed the **minting**, **querying**, and **transferring** of NFTs.

However, we may need a *function* to delete a specific **NFT**, and this deletion is very different from the deletion discussed in the previous section.

In the ***deleteById*** function, deleting was simply removing a specified TokenId from the wallet, but in this *function*, the deletion to be performed is to completely delete the **NFT**, and all its related information must be deleted. 

To accomplish this *function*, in this section, we need to:

1. query the information of the **NFT** based on the tokenId to be transferred.
2. check that it’s the owner trying to delete the **NFT**.

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

  function transfer(address _to, uint256 _tokenId) public {
    require(_to != address(0), "Invalid recipient");
    require(_tokenId >= 1 && _tokenId < nextTokenId, "Invalid token ID");
    Token storage token = tokens[_tokenId];
    require(token.owner == msg.sender, "You don't own this token");
    token.owner = _to;
    deleteById(msg.sender, _tokenId);
    ownerTokens[_to].push(_tokenId);
  }

  //Create a function to get information on a specified NFT
  function getNFT(uint256 _tokenId) public view returns (string memory name, string memory description, address owner) {
    require(_tokenId >= 1 && _tokenId < nextTokenId, "Invalid token ID");
    Token storage token = tokens[_tokenId];

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