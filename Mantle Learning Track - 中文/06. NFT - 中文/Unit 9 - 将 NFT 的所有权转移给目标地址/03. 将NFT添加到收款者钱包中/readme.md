# Content/**将NFT添加到收款者钱包中**

删除数组中的元素确实不是一件容易的事情...

但是，现在让我们来做一些简单的事情吧！我们需要将TokenId添加到收款者的钱包中。

要实现这个目标，我们只需要使用`push`语句将元素添加到*数组*中即可。

**Syntax Review**

variable

- 提示
    
    ```solidity
    arr.push(TokenId)
    ```
    

# Quiz/TODO

# QuizA

1. 先在***ownerTokens**映射*中查询到***_to**地址*对应的钱包，随后使用`push`语句将***_tokenId***添加到*数组*的末端。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.17;

contract MyNFT {
    
    // 定义 Token 结构体，用于存储 NFT 信息
    struct Token {
        string name;        // NFT 名称
        string description; // NFT 描述信息
        address owner;      // NFT 所有者地址
    }
    
    // 使用 mapping 存储每个 NFT 的信息
    mapping(uint256 => Token) private tokens;
    // 使用 mapping 存储每个地址所拥有的 NFT ID 列表
    mapping(address => uint256[]) private ownerTokens;

    // 记录下一个可用的 NFT ID
    uint256 nextTokenId = 1;
    
    // 创建 NFT 函数，用于创建一个新的 NFT，并将其分配给调用者
    function mint(string memory _name, string memory _description) public returns(uint256){ 
        Token memory newNFT = Token(_name, _description, msg.sender);
        uint256 tokenId = nextTokenId;
        tokens[tokenId] = newNFT;
        ownerTokens[msg.sender].push(tokenId);
				nextTokenId++;
        return tokenId;
    }

    // 获取指定 NFT 的信息
    function getNFT(uint256 _tokenId) public view returns (string memory name, string memory description, address owner) {
        require(_tokenId >= 1 && _tokenId < nextTokenId, "Invalid token ID");
        Token storage token = tokens[_tokenId];
        name = token.name;
        description = token.description;
        owner = token.owner;
    }

    // 获取指定地址所拥有的所有 NFT ID
    function getTokensByOwner(address _owner) public view returns (uint256[] memory) {
        return ownerTokens[_owner];
    }

    // 转移指定 NFT 的所有权给目标地址
    function transfer(address _to, uint256 _tokenId) public {
				require(_to != address(0), "Invalid recipien");
				require(_tokenId >= 1 && _tokenId < nextTokenId, "Invalid TokenID");
				
				Token storage token = tokens[_tokenId];
				require(token.owner == msg.sender, "You don't own this token");
				
				token.owner = _to;

				deleteById(msg.sender, _tokenId);
				@@@
				ownerTokens[_to].push(_tokenId);
			  ###
				//regex starts here
				^ownerTokens\s*\[\s*_to\s*\]\s*\.\s*push\s*\(\s*_tokenId\s*\)\s*;\s*$
				//regex ends here
		}

}
```