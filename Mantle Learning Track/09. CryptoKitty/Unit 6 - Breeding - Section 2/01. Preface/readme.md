# Content/Intro

In the previous section, we defined the ***breed*** function, ensured that the caller has the authority to **breed** a new kitty, and retrieved the information of both the cat's mom and dad.

In this section, we can proceed to write how to **breed** the kitty. 

We will calculate the new genes and the generation number, and finally, create the next generation of kitty.

# Example/ Code

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.17;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";

contract SimpleCryptoKitties is ERC721 {
  uint256 public _tokenIdCounter = 1;

  struct Kitty {
    uint256 genes;
    uint256 birthTime;
    uint256 momId;
    uint256 dadId;
    uint256 generation;
  }

  mapping(uint256 => Kitty) public kitties;

  constructor() ERC721("SimpleCryptoKitties", "SCK") {
    createKittyGen0();
    createKittyGen0();
  }

  function _createKitty(
    uint256 momId,
    uint256 dadId,
    uint256 generation,
    uint256 genes,
    address owner
  ) private returns (uint256) {
    kitties[_tokenIdCounter] = Kitty(
      genes,
      block.timestamp,
      momId,
      dadId,
      generation
    );
    _mint(owner, _tokenIdCounter);
    return _tokenIdCounter++;
  }

  function createKittyGen0() private returns (uint256) {
    uint256 genes = uint256(
      keccak256(abi.encodePacked(block.timestamp, _tokenIdCounter))
    );
    return _createKitty(0, 0, 0, genes, msg.sender);
  }

  function breed(uint256 momId, uint256 dadId) public returns (uint256) {
    Kitty memory mom = kitties[momId];
    Kitty memory dad = kitties[dadId];

    require(ownerOf(momId) == msg.sender, "Not the owner of the mom");
    require(ownerOf(dadId) == msg.sender, "Not the owner of the dad");
 
  }
}
```