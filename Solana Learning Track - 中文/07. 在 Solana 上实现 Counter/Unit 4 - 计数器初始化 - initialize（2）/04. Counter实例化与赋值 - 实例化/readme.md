# Content/Counter实例化与赋值

在上一节中，我们成功地获取了 ***Counter*** 账户的可变引用以及 ***bump*** 值。下一步是利用这些信息来初始化 ***Counter*** 结构体的实例。

1. **Counter实例化**

首先，让我们着手创建 ***Counter*** 的实例。回想一下，它有三个关键属性：***authority***、***count*** 和 ***bump*** 。下面，我们来为这些属性赋值：

```rust
Counter {
    authority: //,
    count: //,
    bump: //,
};
```

- ***authority***：这里我们设置这个字段为传入的 ***authority*** 账户的公钥。
    
    ```rust
    ctx.accounts.authority.key
    ```
    
- ***count*** ：这是计数器的起始点，表示在开始时，计数器的值。作为计数器的起始点，我们将 ***count*** 初始化为 0
- ***bump*** ：最后，我们将之前提取的 ***bump*** 值赋给 ***Counter*** 实例。

这样，我们就成功地初始化了 ***Counter*** 结构体的实例，准备好了用于后续操作的基础数据结构。

**Syntax**

counter实例化

- 提示
    
    ```rust
    Counter {
      authority: *ctx.accounts.authority.key,
      count: 0,
      bump,
    };
    ```