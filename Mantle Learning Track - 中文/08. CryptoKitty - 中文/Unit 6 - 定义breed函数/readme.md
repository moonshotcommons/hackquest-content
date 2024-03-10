# Content/引文

在上一节中，我们学习了如何创建创世小猫。那么，如何孕育下一代小猫呢？

本节将介绍***CryptoKitty***合约的第三个功能：孕育小猫。

这个功能是*CryptoKitty*中最有趣的部分。当用户在*CryptoKitty*这款区块链游戏中为自己的小猫找到配偶后，他们可以孕育下一代小猫。这些新生的小猫不仅是独特的，而且它们的基因与其父母紧密相关。

好了，既然已经介绍了这么多，让我们开始实现这个功能吧！

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
}
```