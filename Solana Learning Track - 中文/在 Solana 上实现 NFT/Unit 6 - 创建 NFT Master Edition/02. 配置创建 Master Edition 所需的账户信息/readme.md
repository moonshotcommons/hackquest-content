# Content/定义账户信息

在本节课中，我们将学习如何配置定义 **Master Edition** 所需的账户数组，这个数组包含了用于存储与创建 NFT 的 Master Edition PDA 相关的所有账户信息。

**定义账户数组：**

```rust
pub fn mint_nft(
        ctx: Context<MintNFT>,
        creator_key: Pubkey,
        uri: String,
        title: String) -> Result<()> {
        
		// ... 前面的代码 ...

		let master_edition_infos = vec![
        ctx.accounts.master_edition.to_account_info(),
        ctx.accounts.mint.to_account_info(),
        ctx.accounts.mint_authority.to_account_info(),
        ctx.accounts.payer.to_account_info(),
        ctx.accounts.metadata.to_account_info(),
        ctx.accounts.token_metadata_program.to_account_info(),
        ctx.accounts.token_program.to_account_info(),
        ctx.accounts.system_program.to_account_info(),
        ctx.accounts.rent.to_account_info(),
    ];
}
```

跟添加元数据所需要的账户数组类似**，**创建 **Master Edition** 所需要的账户信息如 ***master_edition***、***mint***、***mint_authority***、***payer*** 等，每个账户都通过 ***to_account_info*** 方法转换为 Solana 的 ***AccountInfo*** 类型。

至此，我们已经配置好了添加 NFT Master Edition 所需的账户信息，下节课，我们就将学习如何创建 **Master Edition**。

**Syntax** 

array

- 提示
    
    ```rust
    let account_info = vec![
            ctx.accounts.my_account_one.to_account_info(),
            ctx.accounts.my_account_two.to_account_info(),
    ];
    ```