# Content/引文

上一节中我们定义了***transfer***函数，进行了参数检查，并且可以获取NFT信息，对NFT拥有者进行访问控制。

本节将在上节基础上，实现**修改NFT拥有者**，将NFT从转账者钱包中**删除**，将NFT添加到收款者钱包中的功能，从而实现完整的**转账**功能。

# Example/ Code

```solidity
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

    function getNFT(uint256 _tokenId) public view returns (string memory name, string memory description, address owner) {
        require(_tokenId >= 1 && _tokenId < nextTokenId, "Invalid token ID");
        Token storage token = tokens[_tokenId];
        name = token.name;
        description = token.description;
        owner = token.owner;
    }

    function getTokensByOwner(address _owner) public view returns (uint256[] memory) {
        return ownerTokens[_owner];
    }

    function transfer(address _to, uint256 _tokenId) public {
				require(_to != address(0), "Invalid recipien");
				require(_tokenId >= 1 && _tokenId < nextTokenId, "Invalid TokenID");
				
				Token storage token = tokens[_tokenId];
				require(token.owner == msg.sender, "You don't own this token");
    }

}
```