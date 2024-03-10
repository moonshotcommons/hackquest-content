# Content/内容

通过上一节的学习我们知道使用`ctx.accounts`可以获取指令函数的账户集合`InitializeAccounts`，它是一个实现了`#[derive(Accounts)]`派生宏的结构体。该派生宏为结构体生成与 Solana 程序账户相关的处理逻辑，以便开发者能够更方便地访问和管理其中的账户。

```rust
// anchor_lang::context
pub struct Context<'a, 'b, 'c, 'info, T> {
    pub accounts: &'b mut T,
    // ...
}

#[program]
mod anchor_counter {
    pub fn initialize(ctx: Context<InitializeAccounts>, instruction_data: u64) -> Result<()> {
        ctx.accounts.counter.count = instruction_data;
        Ok(())
    }
}

#[derive(Accounts)]
pub struct InitializeAccounts<'info> {
    #[account(init, payer = user, space = 8 + 8)]
    pub counter: Account<'info, Counter>,
    // ...
}
```

### #[derive(Accounts)] 宏的介绍

该宏应用于指令所要求的账户列表，实现了给定 struct 结构体数据的反序列化功能，***因此在获取账户时不再需要手动迭代账户以及反序列化操作，并且实现了账户满足程序安全运行所需要的安全检查***，当然，需要`#[account]`宏配合使用。

1、下面我们看下示例中的`InitializeAccounts`结构体，当`initialize`指令函数被调用时，程序会做如下2个校验：

```rust
#[derive(Accounts)]
pub struct InitializeAccounts<'info> {
    #[account(init, seeds = [b"my_seed", user.key.to_bytes().as_ref()], payer = user, space = 8 + 8)]
    pub pda_counter: Account<'info, Counter>,
    #[account(mut)]
    pub user: Signer<'info>,
    pub system_program: Program<'info, System>,
}
```

- **账户类型校验：**传入的账户是否跟`InitializeAccounts`定义的账户类型相匹配，例如Account、Singer、Program等类型。
- **账户权限校验**：根据账户标注的权限，框架会进行相应的权限校验，例如检查是否有足够的签名权限、是否可以修改等。

如果其中任何一个校验失败，将导致指令执行失败并产生错误。

2、`InitializeAccounts`结构体中有如下3种账户类型：

2.1、 `Account`类型：它是`AccountInfo`类型的包装器，可用于验证账户所有权并将底层数据反序列化为Rust类型。对于结构体中的`counter`账户，Anchor 会实现如下功能：

```rust
pub pda_counter: Account<'info, Counter>,
```

① 该账户类型的 Counter 数据自动实现反序列化。

② 检查传入的所有者是否跟 Counter 的所有者匹配。

2.2、`Signer`类型：这个类型会检查给定的账户是否签署了交易，但并不做所有权的检查。只有在并不需要底层数据的情况下，才应该使用Signer类型。

```rust
pub user: Signer<'info>,
```

2.3、`Program`类型：验证这个账户是个特定的程序。对于system_program 字段，Program 类型用于指定程序应该为系统程序，Anchor 会替我们完成校验。

```rust
pub system_program: Program<'info, System>,
```

这里，我们只是对`#[derive(Accounts)]`中的账户的类型进行了介绍，其实每个字段还有`#[account(..)]`属性宏，我们放在下节讲解~

<aside>
💡 总的来说，**`#[derive(Accounts)]`** 是Anchor框架的宏，简化 Solana 程序中的账户处理代码。通过结构体属性标注，自动生成账户操作逻辑，提高可读性和可维护性，使开发者更专注于业务逻辑。

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