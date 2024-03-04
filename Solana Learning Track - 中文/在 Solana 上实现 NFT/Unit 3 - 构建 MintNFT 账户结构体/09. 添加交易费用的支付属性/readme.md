# Content/**定义 `payer` 属性**

这一节课中，我们将学习 ***MintNFT*** 结构体中的 ***payer*** 属性，这个属性在程序的执行过程中起着至关重要的作用，它主要负责支付交易费用和处理其他与资金相关的操作。

**添加 *payer* 属性：**

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
}
```

- 我们将该帐户标记为 `#[account(mut)]`，因为交易时会涉及到交易费用，需要更改帐户的余额。
- `AccountInfo<'info>`：***payer*** 帐户使用 **Anchor** 的 `AccountInfo` 账户类型。`Account` ****帐户类型虽然是一种更安全的帐户声明方式，它也包含 `AccountInfo` 的所有方法，但它适用在需要对账户进行所有权检查、将底层数据反序列化为指定类型的场景。

**Syntax** 

macro struct

- 提示
    
    ```rust
    #[derive(Accounts)]
    pub struct MintNFT<'info> {
        #[account(mut)]
        pub payer_account: AccountInfo<'info>,
    }
    ```