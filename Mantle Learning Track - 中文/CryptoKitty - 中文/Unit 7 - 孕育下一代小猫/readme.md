# Content/引文

上一章我们定义了***breed***函数，并且知道了如何通过函数的参数来获取猫爸猫妈的信息。

在本章中，我们来学学如何利用猫爸猫妈的信息来孕育一个新的小猫吧！

新的小猫应该在基因上和父母的基因有一定的联系，并且“迭代数”也会相应的增加一代。

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

  function createKittyGen0() public returns (uint256) {
    uint256 genes = uint256(
      keccak256(abi.encodePacked(block.timestamp, _tokenIdCounter))
    );
    return _createKitty(0, 0, 0, genes, msg.sender);
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

  function breed(uint256 momId, uint256 dadId) public returns (uint256) {
    require(momId != dadId, "both ids are the same!");
    require(ownerOf(momId) == msg.sender, "Not the owner of the mom kitty");
    require(ownerOf(dadId) == msg.sender, "Not the owner of the dad kitty");
    Kitty memory mom = kitties[momId];
    Kitty memory dad = kitties[dadId];
  }
}
```