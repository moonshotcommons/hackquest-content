# Content/部署合约

由于合约中添加了功能，所以我们需要重复之前的合约部署步骤来部署新的合约。

我们先在本地使用 Remix VM 部署合约测试。

---

**TODO**

1. 点击左侧第一个按钮，再点击“**Compile**”编译合约
2. 点击左侧第二个按钮，再点击“**Deploy**”部署合约

（如果忘了怎么部署，可以翻看之前的教程）

![Untitled](./img/1-1.png)

![Untitled](./img/1-2.png)

# Content/铸造

![Untitled](./img/1-3.png)

为了完成转账，我们首先需要先将NFT铸造出来，还记得铸造的步骤吗？

让我们来试试吧，如果你对此有困惑，请参阅Mint章节。

---

1. 在IDE中完成NFT的铸造

# Content/查询

![Untitled](./img/1-4.png)

![Untitled](./img/1-5.png)

好了，在铸造后，我们已经拥有了一个NFT。

在转账之前，先让我们确认一下我们的钱包状态，如果你对此有困惑，请参阅getTokensByOwner章节。

---

1. 复制当前地址
2. 将其粘贴到***getTokenByOwner***的参数字段
3. 点击函数名调用
    
    > 可以看到我们的钱包目前是有一个***TokenId***为*1*的NFT的
    > 

# Content/查询

![Untitled](./img/1-6.png)

知道了我们拥有这个NFT后，我们再来查询一下这个TokenId为*1*的NFT的详细信息吧！

---

1. 在***getNFT***的参数框输入*1*
2. 点击函数名进行调用
    
    > 可以看到目前NFT的拥有者是”*0x53B3…*”这个地址
    > 

# Content/切换账户并复制账户地址

![Untitled](./img/1-7.png)

到此为止，你应该确认的是“*0x5B38……*”这个账号拥有1个NFT。

接下来我们要将这1个NFT转出，首先我们在**Account**中找到第二个默认地址“*0xAb8…*”。

> 目的是为了复制这个账户的地址
> 

---

1. 点击**ACCOUNT**的展开框
2. 切换到第二个默认账号
3. 复制第二个账号的地址

# Content/切换到原账号

![Untitled](./img/1-8.png)

接下来，我们切换回第一个账号“*0x5B38……*”

---

1. 切换回“*0x5B38……*”账号

# Content/转账

![Untitled](./img/1-9.png)

此时我们应该已经切换回了”*0x5B38……*”的账号，随后就可以使用该地址对刚刚复制的第二个账号”*0xAb8…*”转账了！

---

1. 打开***transfer**函数*的下拉框
2. 将刚刚复制的第二个地址”*0xAb8…”*传入第一个参数
3. 第二个参数填*1*

> 这是要发生转移的NFT的TokenId
> 

# Content/查询

![Untitled](./img/1-10.png)

![Untitled](./img/1-11.png)

非常好！刚刚我们已经完成了转账，

随后我们可以重复在转帐前做的两次查询，来比较转账前后的变化。

首先我们先查询转账者账号“*0x5B38……*”的钱包状态，理论上来讲，该账号的钱包应该是空的，而账号“*0xAb8…*“的钱包内应该有一个TokenId为*1*的NFT。

让我们来验证一下吧！

---

1. 将“*0x5B38…*”账号作为参数调用***getTokenByOwner**函数*
2. 将“*0xAb8…*“账号作为参数调用***getTokenByOwner**函数*

# Content/验证

![Untitled](./img/1-12.png)

接下来我们再来验证一下这个NFT的持有者是否已经变为了刚刚转账的接收者”*0xAb8…*”。

1. 在***getNFT***的参数框输入*1*
2. 点击Call进行调用
    
    > 可以看到该NFT的拥有者是已经转变成了”*0xAb8…*”账号
    > 

# Content/连接账户

很好！到这一步我们已经成功完成了合约的功能测试，确定我们的合约编写无误。我们可以将合约真正部署到链上了！（如果暂时没有部署需求可以跳过接下来的步骤。）

在部署之前，我们需要先连接钱包。本教程中使用 MetaMask 做演示，要完成接下来的步骤，请确保您的浏览器已安装 MetaMask 钱包插件。

---

**TODO**

1. 点击左侧第二个图标
2. 选择 Injected Provider - MetaMask
3. 在Metamask弹出框内点击**Connect**确认将钱包与IDE连接

![Untitled](./img/1-13.png)

# Content/链上部署合约

在连接钱包后，我们准备开始将合约部署上链。本教程使用 Mantle 测试链做演示，要完成接下来的步骤，请确保您的钱包配置并切换到了 Mantle 链，且与 IDE 连接的钱包账户中拥有一定的 MNT 测试币。（当然，如果这些操作不太熟悉的话，可以去翻看我们之前教程，有更加详细的介绍。）

---

**TODO**

1. 点击 Deploy
2. 在 MetaMask 弹出框内点击confirm确认交易

![Untitled](./img/1-14.png)

# Content/查询合约信息

这是一个真正部署上链的合约！你可以去 Mantle 提供的区块链浏览器中查询相关合约信息。 

查看我们部署的合约，让我们把刚刚部署的合约展开，我们应该可以看到里面的所有公开函数和公开变量。

**TODO**

1. 在Deployed Contracts中复制部署的合约地址。
2. 打开 [Mantle 区块链浏览器](https://explorer.testnet.mantle.xyz/)，查询合约信息

![Untitled](./img/1-15.png)

![Untitled](./img/1-16.png)

# Example/示例代码

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
				uint256[] storage ownerTokenList = ownerTokens[msg.sender];
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