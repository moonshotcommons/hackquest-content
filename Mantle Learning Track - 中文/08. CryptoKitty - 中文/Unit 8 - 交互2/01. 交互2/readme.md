# Content/Module

[Crypto-2-output.mp4](./vedio/Crypto-2-output.mp4)

1. 点击Try it Out进入HackQuest IDE。编译并部署合约
2. 调用***createKittyGen0***函数
3. 再次调用***createKittyGen0***函数
4. 查询创建好的两个初代小猫信息
5. 将这两个初代小猫，作为参数调用***bread***函数
6. 查询函数*返回值*
7. 查询新生成的小猫的信息

# Example/示例代码

```solidity
//SPDX-License-Identifier: UNLICENSED
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
    uint256 genes = uint256(keccak256(abi.encodePacked(block.timestamp, _tokenIdCounter)));
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

  function breed(uint256 momId, uint256 dadId) public returns (uint256) {
    Kitty memory mom = kitties[momId];
    Kitty memory dad = kitties[dadId];

    require(ownerOf(momId) == msg.sender, "Not the owner of the mom kitty");
    require(ownerOf(dadId) == msg.sender, "Not the owner of the dad kitty");
    uint256 newGeneration = (mom.generation > dad.generation? mom.generation : dad.generation) + 1;
    uint256 newGenes = (mom.genes + dad.genes) / 2;
    return _createKitty(momId, dadId, newGeneration, newGenes, msg.sender);
  }
}
```