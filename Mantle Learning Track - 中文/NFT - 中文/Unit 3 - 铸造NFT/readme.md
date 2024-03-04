# Content/引文

在前两节我们已经实现了NFT合约的初始化以及状态变量的定义。

现在让我们来给*合约*增加一些功能。首先是***mint***函数，此*函数*的作用是铸造NFT，你只需要输入指定NFT的名字和描述信息，就可以通过此*函数*铸造一个独一无二的NFT。
# Example/ Code
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.17;

contract MyNFT {
    
    // 定义 Token 结构体，用于存储 NFT 信息
    struct Token {
        string name;        // NFT 名称
        string description; // NFT 描述信息
        address owner;      // NFT 所有者地址
    }
    mapping(uint256 => Token) private tokens;
		mapping(address => uint256[]) private ownerTokens;

    // 记录下一个可用的 NFT ID
    uint256 nextTokenId = 1;
```