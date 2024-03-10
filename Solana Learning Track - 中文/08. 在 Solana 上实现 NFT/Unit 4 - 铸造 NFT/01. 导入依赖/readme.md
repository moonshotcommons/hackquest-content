# Content/导入依赖

为了实现我们 NFT 铸造，我们需要导入 anchor_spl 库，它可以通过与 Solana 标准程序库（SPL）的交互，实现代币管理等常见的功能。

1. 导入 `anchor_spl::token` 模块。
    
    ```rust
    use anchor_spl::token;
    ```
    
    它基于 Solana 的代币标准，提供了处理代币相关操作的基础功能。通过导入这个模块，我们就能够在程序中轻松实现代币的创建、转账和查询等操作。
    
2. 导入`anchor_spl::token`模块中的 **MintTo** 和 **Token** 结构体。
    
    ```rust
    use anchor_spl::token::{MintTo, Token};
    ```
    
    - ***MintTo*** 允许我们在程序中铸造新的代币；
    - ***Token*** 是一个代币实例；
    
    这两个结构是我们实现铸造 NFT 功能代码的基础。
    

从下节课开始，我们就将利用导入的程序库来实现我们的 NFT 铸造功能。

**Syntax** 

use

- 提示
    
    ```rust
    use anchor_spl::token;
    ```