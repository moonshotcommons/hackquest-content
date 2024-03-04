# Content/引文

到目前为止，我们已经完成了NFT的**铸造**，**查询**和**转账**。

但我们可能还需要一个功能，可以删除某个NFT，这里的删除和上一节讲的删除有很大的不同。

上一节中的删除只是在钱包中删除指定的TokenId，而这一节中要讲的删除，是将该NFT彻底的删除，他所有相关联的信息都必须删除。为了完成此功能，我们需要以下的步骤：

1. 根据要删除的tokenId查询到该NFT的信息
2. 将该TokenId从拥有者钱包删除
3. 将该NFT从NFT列表中删除

那么此时删除功能就被认为完成了。 在本节结束时，我们将能够在 Remix 中完成NFT的删除。

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
        token.owner = _to;
        
        deleteById(msg.sender, _tokenId);
        ownerTokens[_to].push(_tokenId);
    }

    function deleteById(address account, uint256 _tokenId) internal {
				uint256[] storage ownerTokenList = ownerTokens[account];
				for (uint256 i = 0; i < ownerTokenList.length; i++) {
						if (ownerTokenList[i] == _tokenId) {
                ownerTokenList[i] = ownerTokenList[ownerTokenList.length - 1];
								ownerTokenList.pop();
								break;
						}
			  }
						
		}

}
```