# Content/**定义 `metadata` 属性**

这一节课中，我们将在 ***MintNFT*** 结构体中加入 ***metadata*** 属性，它用于存储和引用 NFT 相关的元数据信息。

**添加 *metadata* 属性：**

```rust
#[derive(Accounts)]
pub struct MintNFT<'info> {
    #[account(mut)]
    pub mint_authority: Signer<'info>,
    #[account(mut)]
    pub mint: UncheckedAccount<'info>,
    pub token_program: Program<'info, Token>,
    #[account(mut)]
    pub metadata: UncheckedAccount<'info>,
}
```

- `#[account(mut)]` ：表示 ***metadata*** 是一个可变的账户引用，因为在 NFT 铸造过程中，账户的状态（如存储的信息）可能会发生变化。

**Syntax** 

macro struct

- 提示
    
    ```rust
    #[derive(Accounts)]
    pub struct MintNFT<'info> {
        pub data: UncheckedAccount<'info>,
    }
    ```