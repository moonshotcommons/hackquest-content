# Content

上一节我们学习了`#[program]`宏，它包含了所有的指令函数，本节我们学习其中的指令函数，以`initialize`函数为例，它的第一个参数为`Context`，这又是什么类型呢？

```rust
#[program]
mod anchor_counter {
    pub fn initialize(ctx: Context<InitializeAccounts>, instruction_data: u64) -> Result<()> {
        ctx.accounts.counter.count = instruction_data;
        Ok(())
    }
}
```

### Context 参数类型

`Context`是 Anchor 框架中定义的一个结构体，用于封装与 Solana 程序执行相关的上下文信息，***包含了 instruction 指令元数据以及逻辑中所需要的所有账户信息***。它的结构如下：

```rust
// anchor_lang::context
pub struct Context<'a, 'b, 'c, 'info, T> {
    /// 当前的program_id
    pub program_id: &'a Pubkey,
    /// 反序列化的账户集合accounts
    pub accounts: &'b mut T,
    /// 不在 accounts 中的账户，它是数组类型
    pub remaining_accounts: &'c [AccountInfo<'info>],
    /// ...
}
```

Context 使用泛型`T`指定了指令函数所需要的账户集合，在实际的使用中我们需要指定泛型 T 的具体类型，如`Context<InitializeAccounts>`、`Context<UpdateAccounts>`等，通过这个参数，指令函数能够获取到如下数据：

- `ctx.program_id`：程序ID，当前执行的程序地址。它是一个 `Pubkey` 类型的值。
- `ctx.accounts`：账户集合，它的类型为泛型 T 所指定的具体类型，如初始化操作所需的账户集合`InitializeAccounts`，更新操作所需的账户集合`UpdateAccounts`，通过派生宏 `#[derive(Accounts)]` 生成。并且 Anchor 框架会为我们自动进行反序列化。
- `ctx.remaining_accounts`：剩余账户集合，包含了当前指令中未被 `#[derive(Accounts)]` 明确声明的账户。它提供了一种灵活的方式，使得程序能够处理那些在编写程序时不确定存在的账户，或者在执行过程中动态创建的账户。其中的账户不支持直接的反序列化，需要手动处理。

### Context<T> 泛型 T

我们先看下第一个指令函数的泛型T：`InitializeAccounts`，该账户集合有3个账户，第1个为数据账户`pda_counter`，它是该程序的衍生账户，用于存储计数器数据；第2个参数为对交易发起签名的账户`user`，支付了该笔交易费；第3个参数为 Solana 系统账户`system_program`，因为PDA账户需要由系统生成，所以我们也需要这个系统账户。

```rust
#[derive(Accounts)]
pub struct InitializeAccounts<'info> {
		// pda 账户
    #[account(init, seeds = [b"my_seed", user.key.to_bytes().as_ref()], payer = user, space = 8 + 8)]
    pub pda_counter: Account<'info, Counter>,
		// 交易签名账户
    #[account(mut)]
    pub user: Signer<'info>,
    pub system_program: Program<'info, System>,
}
```

限于篇幅，对于这些账户的类型及属性，我们放在下节介绍。

### 指令参数（可选）

在 Anchor 框架中，指令函数的第一个参数`ctx`是**必须**的，而第二个参数是指令函数执行时传递的额外数据，是**可选**的，是否需要取决于指令的具体逻辑和需求。在`initialize`中，它被用于初始化计数器的初始值；而在`increment`中，该指令不需要额外的数据，所以只有`ctx`参数。

<aside>
💡 总的来说，**`Context`** 结构体的目的是为开发者提供方便的方式来访问与程序执行相关的信息。通过将这些信息组织在一个结构体中，可以更清晰地管理和访问上下文信息，而不必在函数参数中传递大量的单独参数。

</aside>

# Example/示例代码

这里展示了完整的程序代码。

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
    pub pda_counter: Account<'info, Counter>,
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