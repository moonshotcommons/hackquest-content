# Content/Intro

So far, we have completed the following:

- Token minting
- Token balance querying

Our token system has taken shape, but we have one thing missing: the transfer function that allows users can call it to **transfer** their tokens to others. 

Transactions are crucial for maintaining currency circulation as they facilitate the **transfer** of value between parties.

The **transfer** process includes the following steps:

1. First, we need to check if the caller’s balance is greater than the amount to be **transferred**.
2. Then, update the balance from ***balances** mapping* of both the **sender** and the **receiver**.

# Example/ Code

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.17;

contract MyToken {
  //mapping used to store the balance corresponding to each address
  mapping(address => uint256) private balances;
  //A uint256 variable is used to store the total supply of the token. It is defined as public and can be queried by anyone.
  uint256 public totalSupply;
  //An address variable is used to store the issuer of this token. This is used for some permission control.
  address private owner;

  constructor(uint256 initialSupply) {
    owner = msg.sender;
    mint(msg.sender, initialSupply);
  }

  //function used to mint tokens
  function mint(address recipient, uint256 amount) public {
    //Permission control is implemented
    require(msg.sender == owner, "Only the owner can perform this action");
    balances[recipient] += amount;
    totalSupply += amount;
  }

  //A function used to query the balance corresponding to an address
  function balanceOf(address account) public view returns (uint256) {
    return balances[account];
  }
}
```