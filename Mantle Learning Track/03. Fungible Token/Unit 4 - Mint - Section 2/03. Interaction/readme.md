# Content/Deploy on Remix VM

![Untitled](./img/3-1.png)

1.  Enter *100* as the amount of initial supply tokens.
2.  Click on Deploy.
    
    > Check the interaction in Unit 2 if you forget how to deploy.
    > 

# Content/Check totalSupply

![Untitled](./img/3-2.png)

1. Open the dropdown menu of the ***Mytoken** contract.*
2. Click the ***totalSupply*** button to query the total minted token.

# Content/Switch account

![Untitled](./img/3-3.png)

1. Copy the address of the account.

# Content/Mint

![Untitled](./img/3-4.png)

1. Paste the address to the first *parameter* of the ***mint*** *function*. 
2. Put *100* as the amount.
3. Click on transact.

# Content/Check totalSupply again

![Untitled](./img/3-5.png)

1. Click the ***totalSupply*** button to query the total minted token.
    
    > It should be *200* now
    > 

# Content/Connect Account

> Excellent! *Contract* testing is done, and it's error-free. Now, let's deploy it to the **blockchain**! (Skip if no immediate deployment is needed.)
> 
> 
> Before deployment, connect your wallet. This tutorial uses **MetaMask**, so make sure it's installed in your browser.
> 

![Untitled](./img/3-6.png)

1. Click on the second icon on the left.
2.  Connect Metamask.

# Content/Deploy on Mantle

After connecting your wallet, we're set to deploy the *contract* on the **specified network**, here we choose **Mantle**. Make sure your wallet is configured for Mantle, and the connected account in the IDE has enough MNT tokens. (For detailed instructions, check our previous tutorials.)

![Untitled](./img/3-7.png)

1. Deploy the ***MyToken.so*l**.
2. Confirm the *transaction*.

# Content/Query Contract

> This is a contract deployed on the blockchain! You can check contract details in the Mantle blockchain explorer.
> 

![Untitled](./img/3-8.png)
![Untitled](./img/3-9.png)
![Untitled](./img/3-10.png)

1. Copy the deployed *contract* address from Deployed *Contracts*.
2. Open the [Mantle Blockchain Explorer](https://explorer.testnet.mantle.xyz/) to query contract details.

# Example/Code

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.17;

contract MyToken {
  //mapping used to store the balance corresponding to each address
  mapping (address => uint256) private balances;
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
    totalSupply += amount;
    balances[recipient] += amount;
  }
}
```
