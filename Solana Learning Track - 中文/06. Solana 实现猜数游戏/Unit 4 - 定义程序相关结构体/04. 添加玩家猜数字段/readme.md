# Content/添加 **`guessing_account`** 字段

上节课，我们已经定义了一个程序账户结构体，用于管理程序交互过程中的账户状态。这节课，我们将往结构体添加一个玩家猜数的字段，用来传递玩家的猜数。

**添加字段**

接下来，我们往 ***ProgramAccountContext*** 结构体中添加一个名为 ***guessing_account*** 的字段。

```rust
#[derive(Accounts)]
pub struct ProgramAccountContext<'info> {
    #[account(
        init_if_needed,
        space=8+4,
        payer=payer,
        seeds = [b"guessing pda"],
        bump
    )]
    pub guessing_account: Account<'info, GuessingAccount>,
}
```

`guessing_account: Account<'info, GuessingAccount>`：

- `'info`：是一个生命周期参数，让这个账户引用在整个结构体生命周期内都是有效的。
- `GuessingAccount`：上节课刚学过这个结构体，在这里它是类型参数，指定了这个账户将持有的数据类型。

这里我们还使用 `#[account]` 宏，用来配置了 PDA 账户的各种属性，如初始化方式、占用的空间大小和付款账户等。

> `#[account]` 是 Anchor 框架中的一个属性宏，提供了一种声明式的方式来指定账户的初始化、权限、空间（占用字节数）、是否可变等属性，从而简化了与 Solana 程序交互的代码。
> 

**参数解析：**

1. `init_if_needed`:  通知 Anchor 框架在需要时自动初始化一个派生账户地址 PDA。如果账户尚未初始化，Anchor 会根据提供的其他参数（如 `space` 和 `payer` ）来初始化它。
2. `space=8+4`：指定账户的空间大小为 `8+4` 个字节，前 *8* 个字节为账户类型识别器，用于识别帐户类型，这样 Anchor 就能对账户进行（反）系列化。
    
    接下来的 *4* 个字节为存储在 `GuessingAccount` 帐户类型中的数据分配空间（ `number` 为 `u32` 类型，占用 *4* 字节）。
    
3. `payer=payer`: 指定了支付账户。
4. `seeds = [b"guessing pda"], bump`: 用于生成一个**Program Derived Address** (**PDA**)。

**Syntax**

struct

- 提示
    
    ```rust
    #[derive(Accounts)]
    pub struct MyContext<'a> {
        pub my_account: Account<'a, MyAccount>,
    }
    ```