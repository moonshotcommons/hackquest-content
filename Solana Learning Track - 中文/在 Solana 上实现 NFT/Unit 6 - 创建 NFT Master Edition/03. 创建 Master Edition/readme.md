# Content/创建 **Master Edition**

还记得前面我们学习了如何导入 `create_master_edition_v3` 函数吗？它是 **Metaplex** 框架中的一个函数，用于在 Solana 区块链上创建我们 NFT 的 **Master Edition**。

> `create_master_edition_v3` 函数创建 NFT 的 Master Edition，代表 NFT 的原版，它允许创作者创建有限或无限数量的复制品（Prints），也就是说，通过这个调用，可以设定 NFT 版本的最大铸造数量，从而控制其稀缺性和独特性。
> 

**调用** `create_master_edition_v3` **：**

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

		invoke(
        &create_master_edition_v3(
            ctx.accounts.token_metadata_program.key(),
            ctx.accounts.master_edition.key(),
            ctx.accounts.mint.key(),
            ctx.accounts.payer.key(),
            ctx.accounts.mint_authority.key(),
            ctx.accounts.metadata.key(),
            ctx.accounts.payer.key(),
            Some(0),
        ),
        master_edition_infos.as_slice(),
    )?;
}
```

- ***Some(0)***: 设置最大铸造数量，这里的 *0* 表示没有限制。

通过执行这个操作，我们在区块链上为 NFT 创建了一个 Master Edition，确保了其作为原创版本和拥有复制品的管理。

至此，我们已经完成了我们 NFT 的全部铸造流程，包括铸造初始 NFT 账户，添加元数据，以及创建 **Master Edition** 来对发行量进行管理。接下来，让我们进入交互环节，创建并铸造我们自己的 NFT！

**Syntax** 

function

- 提示
    
    ```rust
    invoke(
            &create_my_metadata(
                // 参数...
            ),
            my_account_info.as_slice(),
    )?;
    ```