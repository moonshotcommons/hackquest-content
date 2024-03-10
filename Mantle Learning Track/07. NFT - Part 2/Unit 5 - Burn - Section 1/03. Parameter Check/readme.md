# Content/Parameter Check

Here, the input *parameter* is TokenId. Do you remember the check we did for TokenId as an input *parameter* in our previous section?

We should ensure that the value of TokenId is within the **NFTs** we have already minted, meaning that TokenId must be greater than *1* but less than ***nextTokenId***.

**Syntax**

require

address

- hint
    
    ```solidity
    require(myId>0 && myId<=10,"it's not within 1-10");
    ```
    
