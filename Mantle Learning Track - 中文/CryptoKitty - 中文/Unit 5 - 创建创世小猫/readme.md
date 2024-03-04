# Content/引文

在上一节中，我们实现了一个创建小猫的通用函数，并详细了解了其功能。在这一节中，我们将继续利用这个通用函数来创建小猫。

本节的目标是实现***CryptoKitty***合约的第二个功能：创建初代小猫。

如果你已经完成了我们的 NFT Guided，那么你可以将本项目视为一个基于 ERC721 的 NFT，只是增加了一些额外的功能。我们需要创建一个结构体来表示每只小猫的基本信息，并将其与 NFT 的 TokenId 关联起来。

这样，我们就可以管理小猫的 NFT。当需要创建初代小猫时，我们只需执行类似于 NFT合约中的 **mint** 操作。

现在，让我们开始实现这个功能吧！

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