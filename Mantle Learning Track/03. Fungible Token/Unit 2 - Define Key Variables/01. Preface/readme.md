# Content/ Intro

In the previous unit, we defined the contract and constructor. Now, we will define a data structure to record the essential information of a token *contract*: every *address's* balance on this token.

Every operation, **minting new tokens**, **transferring**, and **burning**, is about updating this *data structure*.

We also need to define more *variables* to track the total supply of tokens issued and the owner in charge of minting new tokens.  

In specific, we will define three *variables* required for this *contract*:

1. ***_balances*** - represents all users’ balances. 
2. ***_totalSupply*** - represents the total amount of coins minted.
3.  ***_owner*** - represents the contract owner and the coin minting administrator.

Lastly, we will restrict the token's issuer to be the contract's **deployer**.

# Example/ Code

```solidity
pragma solidity 0.8.17;

contract MyToken {
    constructor() { }

}
```