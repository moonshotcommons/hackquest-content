# Content/**定义程序**账户**结构体**

在这一课中，我们将学习如何定义程序账户结构体，它用于管理程序交互过程中的账户状态。

**创建结构体：**

***AccountContext*** 结构体将包含所有必要的账户引用，用于程序的执行。首先，我们定义结构体并使用 `#[derive(Accounts)]` 宏。

```rust
#[derive(Accounts)]
pub struct ProgramAccountContext<'info> {
    // 字段将在此定义
}
```

`#[derive(Accounts)]`： 回顾下前面 Anchor 基础课，我们知道这个派生宏可以实现对给定结构体数据的反序列化，自动生成账户等操作。

> 更详细的解释就是，有了这个派生宏，在获取账户时不再需要手动迭代账户以及反序列化操作，并且实现了账户满足程序安全运行所需要的安全检查。
> 

`<'info>`： 生命周期参数，用于指定结构体中引用的有效期。

**Syntax**

struct

- 提示
    
    ```rust
    #[derive(Accounts)]
    pub struct MyContext<'a> {
        pub my_account: Account<'a, MyAccount>,
    }
    ```