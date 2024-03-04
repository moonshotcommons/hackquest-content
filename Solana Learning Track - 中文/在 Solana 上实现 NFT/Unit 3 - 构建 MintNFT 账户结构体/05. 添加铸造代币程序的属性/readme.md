# Content/**定义** `token_program` **属性**

在这一节课中，我们将在 ***MintNFT*** 结构体中添加另一个重要的属性：***token_program***，它用于处理代币相关操作的程序，在我们 NFT 铸造过程中起到关键作用。

**添加 *token_program* 属性：**

```rust
#[derive(Accounts)]
pub struct MintNFT<'info> {
    #[account(mut)]
    pub mint_authority: Signer<'info>,
    #[account(mut)]
    pub mint: UncheckedAccount<'info>,
    pub token_program: Program<'info, Token>,
}
```

`Program<'info, Token>`：***token_program*** 字段是 `Program` 类型，表示 Solana 上的程序，泛型使用了 `Token` 来指定，说明它是负责执行所有与代币相关的操作，如代币的转移、铸造等。

**Syntax** 

macro struct

- 提示
    
    ```rust
    #[derive(Accounts)]
    pub struct MintNFT<'info> {
        #[account(mut)]
        pub program: : Program<'info, Token>,
    }
    ```