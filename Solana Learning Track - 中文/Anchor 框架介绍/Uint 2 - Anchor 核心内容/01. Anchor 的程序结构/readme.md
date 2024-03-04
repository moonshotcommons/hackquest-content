# Content

> 在前面的章节中我们对 Anchor 有了初步的了解，但似乎并没有发现它给我们的程序开发带来什么便捷之处，接下来我们继续深入 Anchor 的程序结构一探究竟。
> 

在执行完`anchor init my_project`命令后，会自动生成 Anchor 示例项目，其中的`lib.rs`文件是 Anchor 框架的核心模块，包含了许多`macros`宏，这些宏为我们的程序生成 Rust 模板代码以及相应的安全校验。这里主要用到的宏是：

- ***declare_id!***: 声明**程序地址**。该宏创建了一个存储程序地址`program_id`的字段，你可以通过一个指定的`program_id`访问到指定的链上程序。
- ***#[program]***: 程序的**业务逻辑代码**实现都将在`#[program]`模块下完成。
- ***#[derive(Accounts)]***: 由于Solana 账户模型的特点，大部分的参数将以**账户集合**的形式传入程序，在该宏修饰的结构体中定义了程序所需要的账户集合。
- ***#[account]***：该宏用来修饰程序所需要的自定义账户。

### Anchor 框架的结构

我们以右侧代码为例，该程序使用`instruction_one`指令函数接收`u8`类型的数据，并保存在链上`Counter`结构体中。当然，Solana 中一切皆账户，所以`Counter`结构体也是该程序的派生账户 PDA。

**1、导入框架依赖：**这里导入了 Anchor 框架的预导入模块，其中包含了编写Solana 程序所需的基本功能，比如`AnchorDeserialize`和`AnchorSerialize`（反序列化和序列化）、`Accounts`（用于定义和管理程序账户的宏）、`Context`（提供有关当前程序执行上下文的信息，包括账户、系统程序等）…**…**

```rust
// 引入相关依赖
use anchor_lang::prelude::*;
```

**2、*declare_id!宏***：指定 Solana 链上程序地址。当你首次构建 Anchor 程序时，框架会自动生成用于部署程序的默认密钥对，其中相应的公钥即为`declare_id!`宏所声明的程序ID（program_id）。

通常情况下，每次构建 Anchor 框架的 Solana 程序时，program_id 都会有所不同。但是通过`declare_id!`宏指定某个地址，我们就能保证程序升级后的地址不变。这种升级方式比起以太坊中智能合约的升级（使用代理模式），要简单很多。

```rust
// 这里只是示意，实际的 program_id 会有所不同
declare_id!("Fg6PaFpoGXkYsidMpWTK6W2BeZ7FEfcYkg476zPFsLnS");
```

**3、*#[program]宏***：修饰包含了所有程序 instructions 指令的模块，该模块中实现了处理指令的具体业务逻辑，每个`pub`修饰的公共函数，都是一个单独的指令。函数的参数有以下2种：

- 第一个参数为 `Context` 类型，包含了处理该指令的上下文信息。
- 第二个参数为指令的数据，可选。

**4、*#[derive(Accounts)] 派生宏***：定义了 instruction 指令所要求的账户列表。该宏实现了给定结构体`InstructionAccounts`（反）序列化的 Trait 特征，因此在获取账户时不再需要手动迭代账户以及反序列化操作。并且实现了账户满足程序安全运行所需要的安全检查，当然，需要`#[account]`宏配合使用。

**5、*#[account]***：该宏用来修饰程序所需要的自定义账户，它支持定义账户的属性并实现相应的安全校验。这里我们的自定义了一个计数器`Counter`。当然，可以有更复杂的结构，取决于我们的具体业务逻辑。

<aside>
💡 本节大家先对 Anchor 框架有个整体的了解，在接下来的小节，我们会分别介绍其中的每个宏。

</aside>

# Example/示例代码

这里展示了用 Anchor 实现的完整demo程序。

```rust
// 引入 anchor 框架的预导入模块
use anchor_lang::prelude::*;

// 程序的链上地址
declare_id!("3Vg9yrVTKRjKL9QaBWsZq4w7UsePHAttuZDbrZK3G5pf");

// 指令处理逻辑
#[program]
mod anchor_counter {
    use super::*;
    pub fn instruction_one(ctx: Context<InstructionAccounts>, instruction_data: u64) -> Result<()> {
        ctx.accounts.counter.data = instruction_data;
        Ok(())
    }
}

// 指令涉及的账户集合
#[derive(Accounts)]
pub struct InstructionAccounts<'info> {
    #[account(init, seeds = [b"my_seed", user.key.to_bytes().as_ref()], payer = user, space = 8 + 8)]
    pub counter: Account<'info, Counter>,
    #[account(mut)]
    pub user: Signer<'info>,
    pub system_program: Program<'info, System>,
}

// 自定义账户类型
#[account]
pub struct Counter {
    data: u64
}
```