# Content/Intro

In the previous section, we completed the function for creating kitties. 

Breeding the next generation of kitties requires a pair, however, we currently don’t have any kitties. 

In this section, we will create the **first-generation (Gen-0) kitty**. 

To create a **Gen-0 kitty**, we need to generate a random **Gen-0 kitty** with random genes and return its TokenId.

Now, let's start!

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
}
```