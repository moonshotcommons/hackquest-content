# Content/Module

[Crypto-u4-output.mp4](./video/Crypto-u4-output.mp4)

1. Click the Try it Out button. **Compile**, and **deploy** the *contract* in the HackQuest IDE.
    
    > For demonstration purposes, we will set the ***createKittyGen0()*** function as `public` and not call it within the *constructor*.
    > 
    
    > Since we called ***createKittyGen0*** function in the *constructor*, there should be two kitties created already by the time of deployment.
    > 
2. Call the ***creatKittyGen0** function*.
3. Check the *return* value.
4. Query the information of the newly created kitty in the ***kitties*** mapping.

# Example/Code

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
    kitties[_tokenIdCounter] = Kitty(genes, block.timestamp, momId, dadId, generation);
    _mint(owner, _tokenIdCounter);
    return _tokenIdCounter++;
  }

  function createKittyGen0() public returns (uint256) {
    uint256 genes = uint256(
      keccak256(abi.encodePacked(block.timestamp, _tokenIdCounter))
    );
    return _createKitty(0, 0, 0, genes, msg.sender);
  }
}
```