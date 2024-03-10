# Content/引文

到目前为止，我们已经完成了NFT的**铸造**和**查询**。

我们的代币系统已经初见雏形，但要成为真正的代币系统，还需要一个交易功能，即**转账**。转账包括这几个步骤：

1. 根据要转账的***tokenId***查询到该NFT的信息
2. 将该NFT的拥有者转换为接收者
3. 将该***tokenId***从发送者的钱包移除
4. 将该***tokenId***添加到接收者的钱包

如果实现了以上四步那么此时转账就被认为完成了。

在本节中，我们主要完成***transfer***函数的定义、参数检查和访问控制。
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
}
```