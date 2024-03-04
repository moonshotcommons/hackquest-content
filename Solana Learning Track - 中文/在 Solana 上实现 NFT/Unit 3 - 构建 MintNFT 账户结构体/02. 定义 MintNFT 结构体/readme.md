# Content/MintNFT

在这一节中，我们将开始构建 ***MintNFT*** 结构体，这是我们 NFT 铸造功能的重要基础，它将包含所有必要的账户引用，用于程序的执行。

首先，我们定义结构体并使用 `#[derive(Accounts)]` 宏。

```rust
#[derive(Accounts)]
pub struct MintNFT<'info> {}
```

让我们来理解这两行代码的基本构成和作用：

1. `#[derive(Accounts)]`： 回顾下前面 Anchor 基础课，我们知道这个派生宏可以实现对给定结构体数据的反序列化，自动生成账户等操作。
    
    > 更详细的解释就是，有了这个派生宏，在获取账户时不再需要手动迭代账户以及反序列化操作，并且实现了账户满足程序安全运行所需要的安全检查。
    > 
2. `pub struct MintNFT<'info> {}`：这定义了一个名为`MintNFT`的公共结构体。`<'info>`是一个生命周期参数，它在这里表明结构体中的所有引用都必须在同一生命周期内有效。

后面的课程，我们会陆续在这个空结构体内，添加各种字段来表示 NFT 铸造过程中涉及的账户。

**Syntax** 

macro struct

- 提示
    
    ```rust
    #[derive(Accounts)]
    pub struct MintNFT<'info> {}
    ```