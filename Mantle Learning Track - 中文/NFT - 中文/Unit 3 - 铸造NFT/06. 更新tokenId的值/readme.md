# Content/**更新tokenId的值**

每一次铸造后，我们都应该使***nextTokenId***的值加*1*，因为此***nextTokenId***对应着下一个要铸造的NFT的ID。

**Syntax** 

variable

- 提示
    ```
    //这是mint函数的伪代码
    function mint(string memory NFT的名字, string memory 描述信息) public {
        tokens[tokenid指针] = Token(NFT的名字, 描述信息, NFT的铸造者（函数调用者）);
            ownerTokens[NFT铸造者（调用者）].push(tokenid指针);
            tokenid指针++;
    }
    ```