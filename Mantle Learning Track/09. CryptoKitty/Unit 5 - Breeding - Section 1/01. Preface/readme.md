# Content/Intro

In the previous section, we learned how to create first-generation kitties. 

In this section, we'll delve into the implementation of the third function in the CryptoKitty contract: **breeding** kitties.

**Breeding** kitties is one of the most exciting features of **CryptoKitty**. When users find a mate for their kitties in this blockchain game, they can breed the next generation of kitties. These offspring are not only unique but also closely connected to the genes of their parents.

In this unit, we will first

1. Define the *function* header.
2. Ensure that the caller is the owner of both parent kitties.
3. Retrieve the parent kitties’ *struct* from the *mapping*.

Now, after all the explanation, let's implement this *function*.

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
}
```