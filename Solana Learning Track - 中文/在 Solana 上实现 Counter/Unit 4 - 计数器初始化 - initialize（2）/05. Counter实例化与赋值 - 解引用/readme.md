# Content/Counter实例化与赋值

继续我们上一节的内容，我们已经成功创建了 ***Counter*** 实例。现在，我们需要这个新实例赋值给之前获取的账户的引用 ***counter*** 。

1. **解引用**
    
    我们使用解引用操作来更新 ***counter*** 账户的数据。
    
    ```rust
    *counter = counter_instance;
    ```
    
    这里的 `*` 是Rust中的解引用操作符。它的作用是：
    
    - **访问引用指向的数据**：通过解引用 (***counter***)，我们实际上访问并修改了 ***counter*** 的数据，而不是仅仅操作一个指向该数据的引用。
    - **更新账户数据**：赋值操作 (`= counter_instance`) 将我们新创建的 ***Counter*** 实例的数据复制到 ***counter*** 中。这意味着 ***counter*** 账户现在包含了更新后的数据，如初始的计数值和授权用户的公钥。

**Syntax**

counter解引用

- 提示
    
    ```rust
    *counter = Counter {
      authority: *ctx.accounts.authority.key,
      count: 0,
      bump,
    };
    ```