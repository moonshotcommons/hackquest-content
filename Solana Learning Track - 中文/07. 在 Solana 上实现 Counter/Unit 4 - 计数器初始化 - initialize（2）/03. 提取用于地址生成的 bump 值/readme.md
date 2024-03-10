# Content/接收参数信息

接着前面的步骤，下一件事是获取用于生成账户地址的 bump 值。这是确保我们的 ***Counter*** 账户地址既独特又安全的关键环节。

1. **提取用于地址生成的 bump 值**：
    
    要获取与 ***Counter*** 账户相关的 PDA bump 值，我们可以使用`ctx.bumps` ****这个特殊字段。
    
    ```rust
    ctx.bumps.counter;
    ```
    
    <aside>
    💡 `ctx.bumps`用于存储所有在程序调用中使用的 Program Derived Addresses (PDA) 的 bump 值
    
    </aside>
    

通过这两节内容，我们不仅准备好了修改 ***Counter*** 账户的能力，还确保了其地址的唯一性和安全性。

**Syntax**

ctx.bumps

- 提示
    
    ```rust
    let bump = ctx.bumps.counter;
    ```