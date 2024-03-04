# Content/**定义程序模块**

在这一节中，我们将学习如何定义我们的 Solana 智能程序模块。完成这一步骤后，我们就可以在里面编写与区块链交互的核心业务逻辑了。

1. **使用**`#[program]`**宏**：用来定义一个 Solana 程序模块，它包含了程序的相关指令和其他相关操作函数。
    
    ```rust
    #[program]
    ```
    
2. **定义** `metaplex_nft` **模块**：接下来，我们将定义一个名为`metaplex_nft`的模块。在这个模块中，我们将编写核心的业务逻辑和智能合约函数。
    
    ```rust
    #[program]
    pub mod metaplex_nft {}
    ```
    
    声明为 `pub` ****模块，使模块中的内容可以被外部访问和使用。
    
3. **导入父模块中的内容**
    
    ```rust
    #[program]
    pub mod metaplex_nft {
        use super::*;
        // 后续业务逻辑
    }
    ```