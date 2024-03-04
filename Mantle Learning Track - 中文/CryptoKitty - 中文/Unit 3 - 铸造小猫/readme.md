# Content/引文

在本节中，我们将实现 ***CryptoKitty*** 合约的首个功能：为创建小猫提供一个通用函数。

之所以编写这一节，是因为在代码开发过程中，许多地方可能会重复使用相同的逻辑。例如，在我们的 ***CryptoKitty*** 项目中，创建小猫的逻辑是通用的，可能在多个地方都需要创建小猫 NFT。将这一逻辑封装为一个单独的函数可以使得其他部分只需调用此函数即可完成小猫的创建，从而提高代码的可读性，增加代码的复用性，并减少代码的总行数。

此外，这种设计方式也有助于降低*gas*消耗，因为合约代码越简洁，部署时所需的*gas*就越少。

好了，既然已经介绍了这么多，让我们开始实现这个功能吧。

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
}
```