# Content/导入依赖

欢迎来到我们 Solana NFT 课程的第一节课。

首先，我们程序初始化的第一步——导入依赖，在这一步骤中我们将学习如何正确地导入所需的库和模块，确保了我们有合适的工具来编写和运行我们的代码。

本课程将使用强大的 **Anchor** 框架来开发，因此，首要步骤是导入 Anchor 框架的相关依赖。

1. **导入 `anchor_lang` 的 prelude 模块**
    
    ```rust
    use anchor_lang::prelude::*;
    ```
    
    **prelude** 模块里包含了我们后续开发所需要的 Anchor 关键模块和函数。
    
2. **导入 `anchor_lang` 的 invoke 函数**
    
    ```rust
    use anchor_lang::solana_program::program::invoke;
    ```
    
    它可以让我们的程序调用另一个已部署好的外部程序，这在我们后续的铸造 NFT 操作中需要用到。
    

好了，我们已经完成了 Anchor 依赖的导入，下节课，我们将会继续学习程序的初始化。

**Syntax** 

use

- 提示
    
    ```rust
    use anchor_spl::token;
    ```