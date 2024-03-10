# Content/初始化随机数

在这一节中，我们将使用前面学过的 ***generate_random_number*** 函数为游戏生成一个随机目标数字。

**设置目标数字**

```rust
pub fn initialize(ctx: Context<ProgramAccountContext>) -> Result<()> {
    let guessing_account = &mut ctx.accounts.guessing_account;
    guessing_account.number = generate_random_number();
    Ok(())
}
```

- `let guessing_account = &mut ctx.accounts.guessing_account;`：这行代码获取一个可变引用 ***guessing_account***，它是一个可以用来存储数据的账户结构体实例，这样，我们接下来就可以把生成的随机数赋值给它，从而记录下来。
- `Ok(())`：表示初始化成功完成，并返回空元组 `()`。

**Syntax**

function

- 提示
    
    ```rust
    pub fn my_function(ctx: Context<MyContext>) -> Result<()> {
        //......
        Ok(())
    }
    ```