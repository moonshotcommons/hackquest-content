# Content/**定义 `master_edition` 属性**

在这节课中，我们将了解 ***MintNFT*** 结构体中的 ***master_edition*** 属性。这个属性在 NFT 铸造过程中非常关键，它代表了 NFT 的“Master Edition”，用于管理 NFT 的限量发行和维护其元数据的一致性。

> 在 Metaplex  Solana NFT 标准中，**MasterEditions** 的概念就是一个 “主” NFT，用户在其中要指定需要铸造的副本数量、NFT 的元数据信息，确保其稀缺性和独特性。（后面我们会更详细介绍）
> 

**添加 *master_edition* 属性：**

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
		#[account(mut)]
    pub master_edition: UncheckedAccount<'info>,
}
```

**Syntax** 

macro struct

- 提示
    
    ```rust
    #[derive(Accounts)]
    pub struct MintNFT<'info> {
        #[account(mut)]
        pub master_edition: UncheckedAccount<'info>,
    }
    ```