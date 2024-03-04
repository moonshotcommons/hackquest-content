# Content/内容

在通过权限验证后，我们的下一个任务是增加计数器的值。这是 ***Counter*** 程序核心功能，允许用户通过程序逻辑来跟踪和更新计数值。

### **具体步骤**

1. **访问计数器**：
    
    我们需要访问 ***Counter*** 账户：
    
    ```rust
    ctx.accounts.counter
    ```
    
    这里的 ***counter*** 对应于我们之前在 ***Increment*** 结构体中定义的 ***Counter*** 账户引用。
    
2. **修改计数值**：
    
    还记得 ***Counter*** 账户上的 ***count*** 字段吗，在初始化阶段我们将它设置为 *0*，现在我们需要增加它的值。简单的`+1`就可以了
    

**Syntax**

+1

- 提示
    
    ```rust
    ctx.accounts.counter.count += 1;
    ```