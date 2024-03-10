# Content/Intro

In the previous section, we created a *struct* to represent the attributes of a kitty and a *mapping* from TokenId to ***Kitty***, and defined the header of the  ***_createKitty*** function.

In this section, let’s proceed with implementing the *function*. It consists of three steps:

1. create a new kitty and add it to ***kitties** mapping*.
2. Minting the NFT.
3. Return the TokenId.

# Example/ Code

```solidity
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

  constructor() ERC721("SimpleCryptoKitties", "SCK") {}

  function _createKitty(uint256 momId, uint256 dadId, uint256 generation, uint256 genes, address owner) private returns (uint256) { }
}
```