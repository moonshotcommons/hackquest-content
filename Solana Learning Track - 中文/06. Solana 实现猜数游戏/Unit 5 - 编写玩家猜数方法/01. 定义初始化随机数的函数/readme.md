# Content/定义初始化**函数**

在这一节中，我们将学习如何定义初始化随机数的函数，后续我们将在这个函数内初始化我们的随机数，并记录下来。

**创建函数：**

```rust
pub fn initialize_program(ctx: Context<ProgramAccountContext>) -> Result<()> {
    // 函数体将在此实现
}
```

> `Context`是 Anchor 框架中定义的一个结构体，用于封装与 Solana 程序执行相关的上下文信息。
> 

***ctx***：接受一个类型为 `Context<ProgramAccountContext>` 的参数，表示当前的程序上下文。`ProgramAccountContext` 指定了指令函数所需要的账户集合。

***Result<()>***：返回一个`Result`类型，其中`()`表示成功时不返回任何值，而错误情况将返回`Err`。

**Syntax**

function

- 提示
    
    ```rust
    pub fn my_function(ctx: Context<MyContext>) -> Result<()> {
        //......
        Ok(())
    }
    ```