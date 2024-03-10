# Content/引文

在上一章中，我们已经定义了合约的结构，那么既然是一个小猫类型的NFT，我们就需要一些数据结构来存储小猫的属性等信息。

在这一章中，我们将定义出存储小猫的数据结构，在这之后，我们就对***CryptoKitty***这个项目有一个大致的认识了。

# Example/ Code

```solidity
pragma solidity 0.8.17;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";

contract SimpleCryptoKitties is ERC721 {
  constructor() ERC721("SimpleCryptoKitties", "SCK") {}
}
```