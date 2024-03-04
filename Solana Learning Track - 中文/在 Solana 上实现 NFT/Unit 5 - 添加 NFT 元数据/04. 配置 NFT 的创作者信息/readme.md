# Content/配置**创作者信息**

在本节课中，我们将学习创建一个与 NFT 相关的创建者信息数组，它用于存储与 NFT 相关的创建者信息，是定义 NFT 元数据的重要组成部分。

**创建 *creator_arr* 数组：**

在 NFT 元数据中，***creator_arr*** 数组用于记录 NFT 的创作者信息。这些信息对于追踪 NFT 的起源和版权至关重要。

```rust
pub fn mint_nft(
        ctx: Context<MintNFT>,
        creator_key: Pubkey,
        uri: String,
        title: String) -> Result<()> {
        
		// ... 前面的代码 ...

		let account_array = vec![
        ctx.accounts.metadata.to_account_info(),
        ctx.accounts.mint.to_account_info(),
        ctx.accounts.mint_authority.to_account_info(),
        ctx.accounts.payer.to_account_info(),
        ctx.accounts.token_metadata_program.to_account_info(),
        ctx.accounts.token_program.to_account_info(),
        ctx.accounts.system_program.to_account_info(),
        ctx.accounts.rent.to_account_info(),
    ];

		let creator_arr = vec![
            mpl_token_metadata::state::Creator {
                address: creator_key,
                verified: false,
                share: 100,
            },
            mpl_token_metadata::state::Creator {
                address: ctx.accounts.mint_authority.key(),
                verified: false,
                share: 0,
            },
     ];
}
```

***Creator* 中的属性说明：**

- 每个 ***Creator*** 结构体实例代表一个创作者，包括其地址、是否经过验证和其在作品中得到的版税比例。
- ***address***: 创作者的地址。
- ***verified***: 标记创作者的身份是否被确认和验证。在 NFT 市场上，这可以增加 NFT 的可信度。在这个例子中，初始设置为 *false*。
- ***share***: 创作者在版税中所占的比例。

我们定义了两个创作者：

1. 主创作者： ***address*** 字段设置为 ***creator_key***，代表了 NFT 的原始创作者。`share: 100` 表示原创作者拥有所有相关版税的 100%。
2. 协助创作者：也就是被授权帮助执行创作的人，他的 ***address*** 字段设置为 ***ctx.accounts.mint_authority.key()***，代表他是 NFT 的铸造授权者。`share: 0` 表示他在版税中没有份额，通常就是某个协助角色或合作方。

这种多个角色的设置让我们的 NFT 创作信息更加真实，可以看到创作团队中每个成员的角色定位和不同的版税收入。好了，完成了创作者信息的配置，下节课我们要学习的是：与 NFT 元数据相关的符号信息。

**Syntax** 

array

- 提示
    
    ```rust
    let creators = vec![
            Creator {
                address: my_creator_key,
                verified: false,
                share: 100,
            },
            // ... 可能的其他创作者 ...
        ];
    ```