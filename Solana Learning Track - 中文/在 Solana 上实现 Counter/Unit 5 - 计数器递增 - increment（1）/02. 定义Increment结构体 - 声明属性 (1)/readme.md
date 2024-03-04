# Content/属性声明

在上一节中，我们成功地定义了 ***Increment*** 结构体的框架。现在，我们的任务是具体地填充这个结构体，以确保我们能够执行递增的操作。

为了实现递增功能，我们需要关注两个主要方面：

1. **访问计数器**：
    
    首先，我们需要直接访问并修改计数器的数值。这意味着我们的结构体需要包含一个指向 ***Counter*** 账户的引用。
    
    <aside>
    💡 这将允许我们读取当前的计数值，并根据递增操作进行更新。
    
    </aside>
    
2. **权限验证（这一部分将在下一节）**

还记得我们在初始化结构体中怎么实现计数器账户的引用的吗？

- Initialize
    
    ```rust
    #[derive(Accounts)]
    pub struct Initialize<'info> {
        #[account(
            init,
            payer = authority,
            space = Counter::SIZE,
            seeds = [b"counter"],
            bump
        )]
        counter: Account<'info, Counter>,
    }
    ```
    

类似这个，但属性配置稍有不同。初始化完成后，我们只需要关注两点：

- 必须确保能够修改 ***Counter***  账户内的计数值，这里可以使用`mut` 关键字。
- 必须确保精确地定位到之前创建和初始化的特定 ***Counter***  账户，这可以通过指定 PDA（Program Derived Address）来实现，即使用 `seeds` 和 `bump` 参数。
    
    ```rust
    seeds = [b"counter"],
    bump = counter.bump
    ```
    

**Syntax**

#[account(…)]，Struct

- 提示
    
    ```rust
    #[derive(Accounts)]
    pub struct Increment<'info> {
        #[account(
            mut,
            seeds = [b"counter"],
            bump = counter.bump
        )]
        counter: Account<'info, Counter>,
    }
    ```