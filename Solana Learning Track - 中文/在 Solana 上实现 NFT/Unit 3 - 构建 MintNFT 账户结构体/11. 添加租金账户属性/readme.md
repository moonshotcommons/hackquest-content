# Content/**定义 `rent` 属性**

这一节课中，我们将学习 ***MintNFT*** 结构体中的 ***rent*** 属性，它负责 Solana 上的租金系统账户，用于处理账户维护费用

 **关于Solana 账户模型中「租金（Rent）」的概念：**

1. 租金与交易费用不同。用户支付租金以将数据存储在 Solana 区块链上。而交易费用是为了处理网络上的指令而支付的。
2. 与以太坊不同，Solana 会收取在其网络上的账户一笔用于存储数据状态的费用，即租金。租金按照账户所存储的代币余额大小进行定期收费，如果账户无法支付租金，系统将删除这个账户，以减少为那些不再维护的数据花费存储成本。如果账户中的资产超过两年租金的最低余额，那么这个账户可以免交租金。

**添加 *rent* 属性：**

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
		pub rent: AccountInfo<'info>,
}
```

**Syntax** 

macro struct

- 提示
    
    ```rust
    #[derive(Accounts)]
    pub struct MintNFT<'info> {
        #[account(mut)]
        pub rent_account: AccountInfo<'info>,
    }
    ```