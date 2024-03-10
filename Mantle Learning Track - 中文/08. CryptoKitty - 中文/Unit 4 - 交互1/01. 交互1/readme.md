# Content/Module

[Crypto-u3-output.mp4](./video/Crypto-u3-output.mp4)

1. 点击Try it Out进入HackQuest IDE。编译并部署合约
    
    > 出于演示目的，我们将***createKittyGen0***函数设置为`public`，而不是在构造函数中调用它。
    > 
2. 调用***_createKitty***函数, ***momId***为*0*，***dadId***为*0*，***generation***为*1, **genes***为*1234* ，***owner*** 为 部署者地址。
3. 查看返回值
4. 在***kitties***映射中查找刚刚创建的小猫

> 这个映射会在下一节中讲到，你现在只需要知道该映射可以通过TokenId查询到小猫信息即可。
> 

# Example/示例代码

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.17;

import "@openzeppelin/contracts@4.9.3/token/ERC721/ERC721.sol";

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
    kitties[_tokenIdCounter] = Kitty(genes, block.timestamp, momId, dadId, generation);
    _mint(owner, _tokenIdCounter);
    return _tokenIdCounter++;
  }
}
```