# Content/引文

上一节中我们定义了***transfer***函数，进行了参数检查，并且可以获取NFT信息，对NFT拥有者进行访问控制。

本节将在上节基础上，实现修改NFT拥有者，将NFT从转账者钱包中删除，将NFT添加到收款者钱包中的功能，从而实现完整的转账功能。

在上两节中，我们完成了NFT的转账，还记得我们有一个功能是直接调用的其他函数吗？

在这一节中，我们将详细介绍如何将指定的TokenId在某个用户的钱包中删除。

删除操作大致有六步：

1. 获取发送者地址的钱包
2. 遍历钱包
3. 在遍历中判断该NFT是否是发生转移的NFT
4. 找到该NFT后将*数组*的最后一个元素移到该元素的位置
5. 随即删除*数组*的最后一个元素
6. 退出遍历

在本节我们主要学习如何定义***deleteById**函数*并获取发送者地址的钱包，遍历钱包。

在下节中我们将完成剩余四步， 在这两节结束时，你应该非常清楚的理解如何在*数组*中删除某个特定的元素。

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

    // 记录下一个可用的 NFT ID
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
				token.owner = _to;
				deleteById(msg.sender, _tokenId);
				ownerTokens[_to].push(_tokenId);
		}

}
```