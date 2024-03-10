# Content/定义SimpleCryptoKitties合约

在项目的开头，我们首先来定义合约。

刚刚我们提到***CryptoKitties***其实是一个遵循ERC721的NFT，所以我们在定义合约时，需要继承ERC721的标准合约。

> 如果你对ERC721，NFT还没有了解，可以移步我们的NFT教程
> 

**Syntax**

contract,inherit

- 提示
    
    ```solidity
    contract CryptoKitties is ERC721 {}
    ```