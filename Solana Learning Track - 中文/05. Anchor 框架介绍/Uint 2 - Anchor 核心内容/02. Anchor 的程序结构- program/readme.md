# Content

上一节我们对 Anchor 框架中的宏进行了整体介绍，本节我们继续学习其中的`#[program]`宏。

```rust
#[program]
mod program_module_name {
    // ...
}
```

### #[program]宏

该宏定义一个 Solana 程序模块，其中包含了程序的指令（instructions）和其他相关逻辑。它包含如下的功能：

**1、定义处理不同指令的函数：**在程序模块中，开发者可以定义处理不同指令的函数。这些函数包含了具体的指令处理逻辑。上节只有1个指令函数`instruction_one`，本节我们在 #[program] 宏中实现了2个指令函数：`initialize`和`increment`，用来实现计数器的相关逻辑，使其更接近于实际的业务场景。

```rust
#[program]
mod anchor_counter {
    use super::*;
		// 初始化账户，并以传入的 instruction_data 作为计数器的初始值
    pub fn initialize(ctx: Context<InitializeAccounts>, instruction_data: u64) -> Result<()> {
				ctx.accounts.counter.count = instruction_data;
        Ok(())
    }

		// 在初始值的基础上实现累加 1 操作
    pub fn increment(ctx: Context<UpdateAccounts>) -> Result<()> {
        let counter = &mut ctx.accounts.counter;
        msg!("Previous counter: {}", counter.count);
        counter.count = counter.count.checked_add(1).unwrap();
        msg!("Counter incremented. Current count: {}", counter.count);
        Ok(())
    }
}
```

**2、提供与**  **Solana SDK** **交互的功能：**通过 `#[program]` 宏，Anchor 框架提供了一些功能，使得与 Solana SDK 进行交互变得更加简单。例如，可以直接使用 `declare_id`、`Account`、`Context`、`Sysvar` 等结构和宏，而不必手动编写底层的 Solana 交互代码，本单元第一节我们没有使用 Anchor 框架，所以需要手动迭代账户、判断账户权限等操作，现在 Anchor 已经替我们实现了这些功能。

**3、自动生成 IDL（接口定义语言）：**`#[program]` 宏也用于自动生成程序的 IDL。IDL 是用于描述 Solana 程序接口的一种规范，它定义了合约的数据结构、指令等。Anchor 框架使用这些信息生成用于与客户端进行交互的 Rust 代码。

Solana 的 IDL（接口定义语言）和以太坊的 ADSL（Application Binary Interface Description Language）有一些相似之处。它们都是一种用于描述智能合约接口的语言规范，包括合约的数据结构、指令等信息。

<aside>
💡 `#[program]` 宏虽然包含的内容比较多，但语法相对简单，接下来让我们乘胜追击，继续学习`Context`类型✈️✈️✈️

</aside>

# Example/示例代码

这里展示了使用 Anchor 框架实现的计数器程序，实现了计数器的初始化和累加功能。

```rust
// 引入 anchor 框架的预导入模块
use anchor_lang::prelude::*;

// 程序的链上地址
declare_id!("3Vg9yrVTKRjKL9QaBWsZq4w7UsePHAttuZDbrZK3G5pf");

// 指令处理逻辑
#[program]
mod anchor_counter {
    use super::*;
    pub fn initialize(ctx: Context<InitializeAccounts>, instruction_data: u64) -> Result<()> {
        ctx.accounts.counter.count = instruction_data;
        Ok(())
    }

    pub fn increment(ctx: Context<UpdateAccounts>) -> Result<()> {
        let counter = &mut ctx.accounts.counter;
        msg!("Previous counter: {}", counter.count);
        counter.count = counter.count.checked_add(1).unwrap();
        msg!("Counter incremented. Current count: {}", counter.count);
        Ok(())
    }
}

// 指令涉及的账户集合
#[derive(Accounts)]
pub struct InitializeAccounts<'info> {
    #[account(init, seeds = [b"my_seed", user.key.to_bytes().as_ref()], payer = user, space = 8 + 8)]
    pub counter: Account<'info, Counter>,
    #[account(mut)]
    pub user: Signer<'info>,
    pub system_program: Program<'info, System>,
}

#[derive(Accounts)]
pub struct UpdateAccounts<'info> {
    #[account(mut)]
    pub counter: Account<'info, Counter>,
    pub user: Signer<'info>,
}

// 自定义账户类型
#[account]
pub struct Counter {
    count: u64
}
```