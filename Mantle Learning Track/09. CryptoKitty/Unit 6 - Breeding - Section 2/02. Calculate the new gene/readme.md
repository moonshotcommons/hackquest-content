# Content/Calculate the new gene

As mentioned earlier, the gene of the kitty is related to its parents. 

We can use the ***abi.encodePacked*** *function* to encode the average of the parents’ genes and the current timestamp, then apply the ***keccak256*** *function* to generate the hash.

This approach ensures that the new kitty's genes have an element of randomness while still reflecting the genetic influence of its parents.

**Syntax**

abi.encodePacked

- hint
    
    ```solidity
    uint256 ave = gene1 / 2 + gene2 / 2;
    uint256(keccak256(abi.encodePacked(timestamp, ave)));
    ```
    
