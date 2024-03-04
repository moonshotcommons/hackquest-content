# Content/完善**其他字段**

在这一课中，我们将继续完善程序账户结构体中的其他字段。这些字段提供了对付款账户和系统程序的引用，是智能合约功能的关键部分。

1. **添加 *payer* 字段：**表示执行智能合约所需的付款账户。
    
    ```rust
    #[derive(Accounts)]
    pub struct ProgramAccountContext<'info> {
        pub guessing_account: Account<'info, GuessingAccount>,
    
        #[account(mut)]
        pub payer: Signer<'info>,
    }
    ```
    
    - `#[account(mut)]`：表示 *payer* ****是一个可变的账户引用，这是因为执行合约时可能会修改账户状态（例如，扣除手续费）。
    - `Signer<'info>`：*payer* 是 **Signer** 类型，表示对该笔交易进行签名的账户。
2. **添加 *system* 字段：**表示 Solana 系统程序的引用，它提供了执行合约所需的一些基础功能。
    
    ```rust
    #[derive(Accounts)]
    pub struct AccountContext<'info> {
        pub guessing_account: Account<'info, GuessingAccount>,
    
        #[account(mut)]
        pub payer: Signer<'info>,
    
        pub system: Program<'info, System>,
    }
    ```
    

**Syntax**

struct

- 提示
    
    ```rust
    #[derive(Accounts)]
    pub struct MyContext<'a> {
        pub my_account: Account<'a, MyAccount>,
        pub payer: Signer<'a>,
        pub system: Program<'a, System>,
    }
    ```