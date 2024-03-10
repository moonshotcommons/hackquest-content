# Content/**实现 `cpi_ctx` 的创建**

在这一节课中，我们将学习如何在 ***mint_nft*** 函数中创建 ***cpi_ctx***，它是 Anchor 框架提供的 `CpiContext` ****类型 ，封装了与 CPI 相关的所有必要信息，包括要调用的程序和相关的账户。

**创建 *cpi_ctx*：**

在前面两节课，我们已经定义了 ***cpi_program*** 和 ***cpi_accounts***，表示铸造代币要调用的程序和相关的账户，接下来，我们将使用这些变量来构建 ***cpi_ctx***：

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
}
```

`CpiContext::new`: 用于创建一个新的 `CpiContext` 实例。它接受两个参数：***cpi_program***（要调用的程序的账户信息）和 ***cpi_accounts***（CPI 所涉及的账户集合）。

从下节课开始，我们就会使用 ***cpi_ctx***  来实现跨程序调用，创建我们的 NFT。

**Syntax** 

function

- 提示
    
    ```rust
    pub fn my_function(ctx: Context<MyContext>) -> Result<()> {
        let cpi_ctx = CpiContext::new(my_program, my_accounts);.
    }
    ```