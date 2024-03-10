# Content/Intro

We have completed the mint function, now we can try to compile and deploy this code for interaction, which will help us gain a deeper understanding of its functionality.

Before compiling, we can also call this *function* in the constructor to **mint** some initial tokens for the **deployer**.

**Minting** the initial supply of tokens to the issuer provides them with an initial allocation for distribution.

# Example/ Code

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.17;

contract MyToken {
  //mapping used to store the balance corresponding to each address
  mapping(address => uint256) private balances;
  //A uint256 variable is used to store the total supply of the token. It is defined as public and can be queried by anyone.
  uint256 public totalSupply;
  //An address variable is used to store the issuer of this token. This is used for some permission control
  address private owner;

  constructor() {
    owner = msg.sender;
  }

  //function used to mint tokens
  function mint(address recipient, uint256 amount) public {
    //Permission control is implemented
    require(msg.sender == owner, "Only the owner can perform this action");
    balances[recipient] += amount;
    totalSupply += amount;
  }
}
```