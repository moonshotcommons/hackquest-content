# Content/**实现** `cpi_program` **的创建**

在这一节课中，我们将学习如何在 ***mint_nft*** 函数中获取 ***cpi_program***，这是我们实现跨程序调用（CPI）的关键。

**什么是 *cpi_program* ？**

> ***cpi_program*** 代表了要调用的外部程序。在我们的铸造 NFT 场景中，指向 Solana 的 **Token Program**，负责处理代币铸造相关的操作。
> 

> **Token Program** 是 Solana 生态系统中的一个核心程序，它提供了一套标准的接口和方法来创建和管理代币，包括 SPL 代币（Solana Program Library tokens）。这个程序负责处理代币的发行、转账、铸造等操作。
> 

**定义** ***mint_nft* 函数：**

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
}
```

- `ctx.accounts.token_program`：这是通过 Anchor 框架 ***Context*** 传递(***MintNFT***)的 Token Program 的引用 - ***token_account***。
- `.to_account_info()` **：**将 Anchor 包装账户 ***token_account*** 转换为 **Solana** 原生的 `AccountInfo` 类型。
    
    `AccountInfo` 是 **Solana** 程序之间进行交互时使用的基本账户类型，当我们进行跨程序调用时，需要统一转换为这种基本类型。
    

通过将 ***token_account*** （Token Program）账户转换为 `AccountInfo` 并赋值给 ***cpi_program***，那么从下节课开始，我们就能够在 ***mint_nft*** 函数中实现与 **Token Program** 的交互，执行铸造代币等关键操作。

**Syntax** 

struct

- 提示
    
    ```rust
    pub fn my_function(ctx: Context<MyContext>) -> Result<()> {
        let cpi_program = ctx.accounts.my_external_program.to_account_info();
    }
    ```