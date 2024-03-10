# Content/Parameter Check for tokenId

After checking **the recipient address** is valid, another check that needs to be done is the validity of the **TokenId**.

We should ensure that the TokenId value is in the NFTs we have already minted, that is, TokenId must be greater than *1* but less than ***nextTokenId***.

**Syntax**

require, address

- hint
    
    ```solidity
    require(amount <= balances[msg.sender]);
    ```
    
