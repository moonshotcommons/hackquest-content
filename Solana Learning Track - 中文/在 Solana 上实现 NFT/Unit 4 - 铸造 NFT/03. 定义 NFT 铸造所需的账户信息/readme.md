# Content/**实现 `cpi_accounts` 的创建**

在这一节课程中，我们将学习如何在 ***mint_nft*** 函数中创建并赋值 ***cpi_accounts***，它包含了我们 NFT 铸造操作所需的账户信息，是 NFT 铸造操作的必要信息。

**什么是 CPI ？**

> CPI 在 Solana 编程和 Anchor 框架中指的是 "Cross-Program Invocation"，即跨程序调用。这是 Solana 智能合约（程序）之间交互的一种机制，允许一个程序（合约）调用另一个已经部署在 Solana 区块链上的程序的函数或方法。
> 

> 在很多场景都会应用到，比如在处理代币交易、读写数据到链上、或者与其他智能合约交互等场合。
> 

> 例如，在 NFT 铸造的过程中，一个程序需要调用 Solana 的 Token Program 来创建新的代币或修改代币的状态。这就是通过 CPI 来实现的，即一个程序（NFT 铸造程序）调用另一个程序（Token Program）的功能。
> 

**定义** ***cpi_accounts* 账户结构体实例：**

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
}
```

`cpi_accounts` **的作用：** 它是一个 ***MintTo*** 结构体的实例，包含了进行 NFT 铸造操作所需的账户信息，为接下来进行跨程序调用做准备。

- ***mint***：指向 NFT 的 mint 账户，用于铸造 NFT。
- ***to***：接收铸造 NFT 的目标账户。
- ***authority***：执行铸造操作的授权账户，通常是支付交易费用的账户。

至此，我们已经定义好了 NFT 铸造所需的账户信息。下一节课，我们将学习另一个铸造操作所需的必要信息 - **代币铸造程序**。

**Syntax** 

struct

- 提示
    
    ```rust
    pub fn my_function(ctx: Context<MyContext>) -> Result<()> {
        let cpi_accounts = MyCpiStruct {
            account_one: ctx.accounts.account_one.to_account_info(),
            account_two: ctx.accounts.account_two.to_account_info(),
        };
    }
    ```