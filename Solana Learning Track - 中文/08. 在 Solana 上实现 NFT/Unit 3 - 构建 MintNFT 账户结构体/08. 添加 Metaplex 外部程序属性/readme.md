# Content/**定义 `token_metadata_program` 属性**

在本节课中，我们将往 ***MintNFT*** 结构体中添加 ***token_metadata_program*** 属性，它指向一个处理元数据相关的程序，由于我们项目是基于 **Metaplex** 协议（后面课程会详细介绍）进行 NFT 开发，因此 ***token_metadata_program*** 指向一个 **Metaplex** 的元数据程序。

**添加 *token_metadata_program* 属性：**

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
    #[account(mut)]
    pub token_account: UncheckedAccount<'info>,
		pub token_metadata_program: UncheckedAccount<'info>,
}
```

> 这个程序负责管理和存储与 NFT 相关的所有元数据，比如 NFT 的描述、作者信息等。
> 

**Syntax** 

macro struct

- 提示
    
    ```rust
    #[derive(Accounts)]
    pub struct MintNFT<'info> {
        #[account(mut)]
        pub metadata_program: UncheckedAccount<'info>,
    }
    ```