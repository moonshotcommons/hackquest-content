# Content/Intro

We have just completed the definition of the ***SimpleCryptoKitties** contract* and defined a variable to track the number of NFTs we’ve minted. 

The key feature that makes **CryptoKitties** different from other ****NFT projects is that the users can **breed** new kitties (create new NFTs) based on the kitties they own.

Therefore, we will first implement the most important *function* in the *contract*:  creating a new Kitty given the genetic information.

Before that, let’s:

1. define a Kitty struct to represent the information of each Kitty.
2. associate each Kitty with its corresponding NFT’s TokenID using a mapping.
3. define a *function* for creating a new kitty.

Now, let's start!

# Example/ Code

```solidity
pragma solidity 0.8.17;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";

contract SimpleCryptoKitties is ERC721 {

  uint256 public _tokenIdCounter = 1;

  constructor() ERC721("SimpleCryptoKitties", "SCK") {}
}
```