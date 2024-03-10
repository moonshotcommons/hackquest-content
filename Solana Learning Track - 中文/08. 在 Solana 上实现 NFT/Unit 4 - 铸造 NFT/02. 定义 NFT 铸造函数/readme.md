# Content/定义 **`mint_nft` 函数**

在这一节中，我们将学习如何在 ***metaplex_nft*** 模块中定义 ***mint_nft*** 函数，后续我们就将在这个函数内完成铸造 NFT 的核心代码。

**定义** ***mint_nft* 函数：**

```rust
#[program]
pub mod metaplex_anchor_nft {
    // ... 其他代码 ...

    pub fn mint_nft(
        ctx: Context<MintNFT>,
        creator_key: Pubkey,
        uri: String,
        title: String,
    ) -> Result<()> {
        // 函数实现...
    }
}
```

**函数参数：**

- `ctx: Context<MintNFT>`：这是一个包含所有必要账户信息的上下文，用于后续执行 NFT 的铸造操作。
- `creator_key: Pubkey`：创建者的公钥，代表了 NFT 的创建者。
- `uri: String`：NFT 元数据的 **URI**，通常是指向描述 NFT 详细信息的外部链接。
- `title: String`：NFT 的标题。

 

从下节课开始，我们就将一步步完成 ***mint_nft*** 函数的功能代码，包括创建新的 NFT，设置 NFT 的元数据，以及管理 NFT 的铸造和发行。

**Syntax** 

function

- 提示
    
    ```rust
    pub fn my_function(ctx: Context<MyContext>) -> Result<()> {
        Ok(())
    }
    ```