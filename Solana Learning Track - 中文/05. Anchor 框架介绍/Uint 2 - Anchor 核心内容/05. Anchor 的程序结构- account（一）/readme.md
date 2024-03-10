# Content/内容

> 通过上一节对**`#[derive(Accounts)]`**派生宏的学习，我们知道 Anchor 为我们提供了针对不同***账户类型的验证***，这些账户类型包括：`Account`、`Singer`、`Program`，更多地账户类型，可以看 [这里](https://docs.rs/anchor-lang/latest/anchor_lang/accounts/index.html)。
> 

这一节，我们来介绍 Anchor 为我们实现的***账户属性约束***：**`#[account(..)]`**。

```rust
#[derive(Accounts)]
struct ExampleAccounts {
  #[account(
    seeds = [b"example_seed"],
    bump
  )]
  pub pda_account: Account<'info, AccountType>,
  
	#[account(mut)]
  pub user: Signer<'info>,
}
```

### **#[account(..)]** 宏的介绍

它是 Anchor 框架中的一个属性宏，提供了一种声明式的方式来指定账户的初始化、权限、空间（占用字节数）、是否可变等属性，从而简化了与 Solana 程序交互的代码。也可以看成是一种账户属性约束。

**1、初始化一个派生账户地址 PDA ：**它是根据`seeds`、`program_id`以及`bump`动态计算而来的，其中的`bump`是程序在计算地址时自动生成的一个值（Anchor 默认使用符合条件的第一个 bump 值），不需要我们手动指定。

```rust
#[account(
	init, 
	seeds = [b"my_seed"], 
	bump,
	payer = user, 
	space = 8 + 8
)]
pub pda_counter: Account<'info, Counter>,
pub user: Signer<'info>,

```

- ***init：***Anchor 会通过相关属性配置初始化一个派生帐户地址 PDA 。
- ***seeds：***种子（seeds）是一个任意长度的字节数组，通常包含了派生账户地址 PDA 所需的信息，在这个例子中我们仅使用了字符串`my_seed`作为种子。当然，也可以包含其他信息：如指令账户集合中的其他字段`user`、指令函数中的参数`instruction_data`，示意代码如下：

```rust
#[derive(Accounts)]
#[instruction(instruction_data: String)]
pub struct InitializeAccounts<'info> {
		#[account(
			init, 
			seeds = [b"my_seed", 
							 user.key.to_bytes().as_ref(),
							 instruction_data.as_ref()
							]
			bump,
			payer = user, 
			space = 8 + 8
		)]
		pub pda_counter: Account<'info, Counter>,
		pub user: Signer<'info>,
}
```

- ***payer：***指定了支付账户，即进行账户初始化时，使用`user`这个账户支付交易费用。
- ***space：***指定账户的空间大小为16个字节，前 8 个字节存储 Anchor 自动添加的鉴别器，用于识别帐户类型。接下来的 8 个字节为存储在`Counter`帐户类型中的数据分配空间（`count`为 u64 类型，占用 8 字节）。

**2、验证派生账户地址 PDA ：**有些时候我们需要在调用指令函数时，验证传入的 PDA 地址是否正确，也可以采用类似的方式，只需要传入对应的`seeds`和`bump`即可，Anchor就会按照此规则并结合`program_id`来计算 PDA 地址，完成验证工作。注意：这里不需要`init`属性。

```rust
#[derive(Accounts)]
#[instruction(instruction_data: String)]
pub struct InitializeAccounts<'info> {
		#[account(
			seeds = [b"my_seed", 
							 user.key.to_bytes().as_ref(),
							 instruction_data.as_ref()
							]
			bump
		)]
		pub pda_counter: Account<'info, Counter>,
		pub user: Signer<'info>,
}
```

**3、`#[account(mut)]`属性约束：**

- ***mut：***表示这是一个可变账户，，即在程序的执行过程中，这个账户的数据（包括余额）可能会发生变化。在Solana 程序中，对账户进行写操作需要将其标记为可变。

以上是我们常用的属性约束，Anchor 为我们提供了许多这样的属性约束，可以看 [这里](https://docs.rs/anchor-lang/latest/anchor_lang/derive.Accounts.html)。

<aside>
💡 总的来说，`#[account(..)]` 宏在 Solana 的 Anchor 框架中用于声明性地配置账户属性。通过宏中的参数，开发者可以指定账户是否可初始化、是否可变、是否需要签名、支付者、存储空间大小等，更重要的是，通过`seeds`属性，可以方便地生成程序派生账户（PDA），将种子信息与程序 ID 结合动态计算账户地址。这使得代码更加清晰、易读，并帮助开发者遵循 Solana 的账户规范，提高了程序的可维护性和可读性。

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
#[instruction(instruction_data: String)]
pub struct InitializeAccounts<'info> {
    #[account(
			init, 
			seeds = [b"my_seed", user.key.to_bytes().as_ref(), instruction_data.as_ref()], 
			payer = user, 
			space = 8 + 8)]
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