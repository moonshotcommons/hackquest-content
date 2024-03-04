# Content/引文

在上一节中，我们学习了如何实现 铸造NFT 的功能，其中还包括部署合约。

铸造新的 NFT 后，一个很自然的步骤是**查询**我们新铸造的 NFT 的信息。 因此，我们会在本节中实现一个查询函数，通过给定的***TokenId***，我们会找到与NFT相关的信息，并将其*返回*给函数调用者。

在本节中，我们将学习如何：

1. 检索指定的 NFT 信息
2. 确保***TokenId***有效
3. 返回NFT信息

# Example/ Code
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.17;

contract MyNFT {
    
    struct Token {
        string name;        // NFT 名称
        string description; // NFT 描述信息
        address owner;      // NFT 所有者地址
    }
    
    mapping(uint256 => Token) private tokens;
		mapping(address => uint256[]) private ownerTokens;


    uint256 nextTokenId = 1;
    
    function mint(string memory _name, string memory _description) public returns(uint256){ 
        Token memory newNFT = Token(_name, _description, msg.sender);
        uint256 tokenId = nextTokenId;
        tokens[tokenId] = newNFT;
        ownerTokens[msg.sender].push(tokenId);
				nextTokenId++;
        return tokenId;
    }

}
```