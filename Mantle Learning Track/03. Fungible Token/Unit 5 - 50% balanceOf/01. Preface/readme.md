# Content/Intro

In the previous section, we implemented the token **minting** function. 

Do you remember how we determined the success of **minting** in the end? We queried the value of the ***totalSupply*** *variable*, but technically we should have checked if the balance of the receiver address increased by the **minted amount**. So, we need another function to implement **balance querying**.

The querying process includes the following steps:

1. First, we need to receive an address as an input of our query *function*.
2. retrieve the corresponding balance from the ***balances*** *mapping* and *return* it. 

With these steps, the balance query is completed. By the end of this section, we will be able to query the balance of any *address* through this *function* using Remix.

# Example/ Code

```solidity
pragma solidity 0.8.17;

contract MyToken {
  //mapping used to store the balance corresponding to each address
  mapping(address => uint256) private balances;
  //A uint256 variable is used to store the total supply of the token. It is defined as public and can be queried by anyone.
  uint256 public totalSupply;
  //An address variable is used to store the issuer of this token. This is used for some permission control.
  address private owner;

  constructor(uint256 initialSupply) {
    mint(msg.sender, initialSupply);
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