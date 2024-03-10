# Content/**实现`token::mint_to` 调用**

经过前面几节课的学习，我们已经配置了与代币铸造相关的程序和账户，并进行了封装，接下来，我们将实现在 Solana 上铸造 NFT 的功能。

> 我们使用 Anchor 框架提供的 **`token::mint_to`** 函数来铸造新的NFT，它对 Solana 的 Token Program 的封装，用于创建新代币。
> 

调用 ****`token::mint_to`**：**

```rust
pub fn mint_nft(
        ctx: Context<MintNFT>,
        creator_key: Pubkey,
        uri: String,
        title: String) -> Result<()> {
        
		let cpi_accounts = MintTo {
	      mint: ctx.accounts.mint.to_account_info(),
        to: ctx.accounts.token_account.to_account_info(),
        authority: ctx.accounts.payer.to_account_info(),
    };

		let cpi_program = ctx.accounts.token_program.to_account_info();
		let cpi_ctx = CpiContext::new(cpi_program, cpi_accounts);
		token::mint_to(cpi_ctx, 1)?;
}
```

**解析：**

- 这个函数负责在指定的 ***mint*** 账户上创建指定数量的代币。在我们使用场景里，铸造数量为 `1` 的代币，也就是铸造一个新的 NFT。
- `cpi_ctx` ：封装了 mint 账户、接收账户和授权账户等信息。

至此，我们已经完成了 NFT 的铸造，但这仅仅只是开始，因为我们铸造的 NFT 跟普通的代币并没有什么区别，一个完整的、独一无二的 NFT 还需要有创作者、名称和图片等信息标记。

从下节课开始，我们就将学习如何向铸造完成的 NFT 添加元数据。

**Syntax** 

function call

- 提示
    
    ```rust
    pub fn my_function(ctx: Context<MyContext>) -> Result<()> {
        token::mint_to(cpi_ctx, amount)?;
    }
    ```