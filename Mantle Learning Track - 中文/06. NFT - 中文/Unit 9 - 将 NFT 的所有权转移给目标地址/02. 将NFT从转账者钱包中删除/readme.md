# Content/**将NFT从转账者钱包中删除**

在修改了NFT的拥有者之后，我们还需要更新转账者和收款者的钱包信息。

让我们首先修改转账者的钱包。我们需要做的是从转账者的钱包数组中**删除**该NFT的TokenId。

然而，数组的删除操作并不像映射中的删除操作那样简单。

在映射中，通过键就可以直接找到要删除的元素并删除，但是在数组中，元素是按顺序连续存储的，而只有第一个元素的位置会被记录。因此，要删除指定的元素，我们需要遍历整个*数组*来找到并移除该元素。（如图）

![未命名白板 (1).jpg](../%E3%80%90Guided%E3%80%91NFT%20-%20transfer%20(1)%20a237833c66f9459e9ad5d22544093780/%25E6%259C%25AA%25E5%2591%25BD%25E5%2590%258D%25E7%2599%25BD%25E6%259D%25BF_(1).jpg)

![mapping.jpg](../%E3%80%90Guided%E3%80%91NFT%20-%20transfer%20(1)%20a237833c66f9459e9ad5d22544093780/mapping.jpg)

为了实现这样的删除操作，并在后续的步骤中多次使用它，我们将其作为一个单独的函数进行定义（我们将在下一节中介绍）。

以下是该*函数*的代码。如果你感兴趣，可以仔细研究一下。

- code
    
    ```solidity
    function deleteById(address account, uint256 _tokenId) internal {
            uint256[] storage ownerTokenList = ownerTokens[account];
            for (uint256 i = 0; i < ownerTokenList.length; i++) {
                if (ownerTokenList[i] == _tokenId) {
                    // 将该 NFT ID 与数组最后一个元素互换位置，然后删除数组最后一个元素
                    ownerTokenList[i] = ownerTokenList[ownerTokenList.length - 1];
                    ownerTokenList.pop();
                    break;
                }
            }
        }
    ```
    

在这里，我们只需要调用这个***deleteById**函数*即可。它需要传入两个参数：要删除的钱包拥有者地址和要删除的NFT的TokenId。

**Syntax** 

variable

- 提示
    
    ```solidity
    //调用删除函数
    deleteById(msg.sender, id);
    ```
    

# Quiz/TODO

# QuizA

1. 调用***deleteById**函数*，第一个*入参*为`msg.sender`，第二个*入参*为***_tokenId***

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
				@@@
				deleteById(msg.sender, _tokenId);
				###
				//regex starts here
				^deleteById\s*\(\s*msg\s*\.\s*sender\s*,\s*_tokenId\s*\)\s*;\s*$
				//regex ends here
    }

}
```