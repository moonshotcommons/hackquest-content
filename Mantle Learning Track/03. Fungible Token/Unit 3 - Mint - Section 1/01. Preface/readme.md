# Content/ Intro

In the previous section, we defined three *variables* and set the ***owner*** to be the deployer. 

However, currently, no one holds any tokens. Therefore, first, we need to create a function to issue tokens. It’s important to note that if anyone can issue tokens, it will lead to chaos.

So, who can be the issuer?

The *contract's* deployer, acting as the administrator, can call this *function* to **mint** tokens to a specified address. 

In this unit, we will finish the minting function. In specific: 

1. define the ***mint*** *function*.
2. check if the caller is the ***owner***.
3. update relevant *variables* includes ***balances*** and ***totalSupply***.

Let’s start!

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
}
```