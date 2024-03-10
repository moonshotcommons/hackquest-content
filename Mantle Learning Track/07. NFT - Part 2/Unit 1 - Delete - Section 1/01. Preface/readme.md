# Content/Intro

So far, we have completed the **minting** and **querying** of NFTs.

Our token system has taken shape, but to become an actual one, it still requires **a transaction function** and a *function* to **destroy** an NFT. Both of these *functions* need to remove a specified NFT with a given TokenId from the user's wallet.

Therefore, we define a separate *function*, named ***deleteById***.

To delete a specified TokenId in a user's wallet, in this section, we will:

1. Define the ***deleteById** funciton*.
2. Get the wallet of the sender's address.
3. Traverse the wallet
    - Why do we traverse the wallet?
        
        We need to remove the TokenId of this NFT from the wallet ***ownerTokens***.
        
        However, it is not an easy task because the wallet is stored as an array, and removing a specified element from an *array* is not as simple as deleting an element from a mapping using the `delete` keyword.
        
        In a *mapping*, each element has a unique key, and these keys are converted into an index value through **a hash function** to determine the position of an element in memory, so it is not necessary to traverse the entire *mapping* when looking for an element. 
        
        By contrast, in an *array*, elements are stored sequentially in continuous *memory* space, and only the position of the first element in the *array* is recorded, so when deleting a specific element, we need to traverse the entire *array* from the first element to find and remove that element (as shown in the image below).
        
        ![image.png](Preface%207989767c302e4924b30b635974fe4776/image.png)
        
        ![image (1).png](Preface%207989767c302e4924b30b635974fe4776/image_(1).png)
        
        Therefore, we cannot directly find a specific element by its key like in a mapping. We must use a method called traversal search to retrieve the element we want, which in this case is the TokenId of the NFT.
        
4. Determine if the NFT being traversed is the NFT that has been transferred.

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
    Token storage token = tokens[_tokenId];
    name = token.name;
    description = token.description;
    owner = token.owner;
  }

  // Get all NFT IDs owned by a specified address
  function getTokensByOwner(address _owner) public view returns (uint256[] memory) {
    return ownerTokens[_owner];
  }
}
```