# Content/Module

[Crypto-u3-output.mp4](./video/Crypto-u3-output.mp4)

1. Click the Try it Out button. **Compile**, and **deploy** the contract in the HackQuest IDE.
    
    > For demonstration purposes, we set the visibility of the ***_createKitty*** function to `public`.
    > 
2. In the IDE interface, open the dropdown menu for the deployed *contract*. Find the ***_createKitty*** *function* and fill in *0* for ***momId***, *0* for ***dadId***, *1* for ***generation***, and *1234* for ***genes***. Copy and paste the caller's *address* into the ***owner*** field. Then, click the call button.
3. Query the kitty’s information using the ***kitties*** mapping.

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

  constructor() ERC721("SimpleCryptoKitties", "SCK") {}

  function _createKitty(
    uint256 momId,
    uint256 dadId,
    uint256 generation,
    uint256 genes,
    address owner
  ) public returns (uint256) {
    kitties[_tokenIdCounter] = Kitty(genes, block.timestamp, momId, dadId, generation);
    _mint(owner, _tokenIdCounter);
    return _tokenIdCounter++;
  }
}
```