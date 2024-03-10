# Content/**定义 `token_account` 属性**

在这一节中，我们将向 ***MintNFT*** 结构体中添加 ***token_account*** 属性。这个属性代表了与即将被铸造的 NFT 相关联的代币账户，简而言之，就是程序会将新铸造出来的 NFT 发送到 ***token_account*** 指定的账户。

**添加 *token_account* 属性：**

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
}
```

**Syntax** 

macro struct

- 提示
    
    ```rust
    #[derive(Accounts)]
    pub struct MintNFT<'info> {
        #[account(mut)]
        pub receive_account: UncheckedAccount<'info>,
    }
    ```