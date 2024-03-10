# Content/**定义 `system_program` 属性**

这一节课中，我们将学习 ***MintNFT*** 结构体中的 ***system_program*** 属性，它主要负责创建所有的账户。

**添加 *system_program* 属性：**

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
		#[account(mut)]
    pub payer: AccountInfo<'info>,
		pub system_program: Program<'info, System>,
}
```

- `Program<'info, System>`：***system_program*** 使用 `Program` 类型，指 Solana 的系统程序（System Program），它是 Solana 区块链的基础组成部分，提供了一系列底层功能，如账户的创建、管理和资金的转移。
    
    在我们项目中定义 ***system_program*** ，是利用系统程序的基础功能，实现账户的创建和修改。
    

**Syntax** 

macro struct

- 提示
    
    ```rust
    #[derive(Accounts)]
    pub struct MintNFT<'info> {
        #[account(mut)]
        pub system: AccountInfo<'info>,
    }
    ```