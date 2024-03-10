# Content/添加随机数字段

上节课，我们已经定义了一个存储猜数数据的结构体。这节课，我们将往结构体添加一个猜数字段，用来记录玩家的猜数，后续我们就可以对比猜数是否正确。

**添加字段**

这个结构体将包含一个存储数字的字段。

```rust
#[account]
pub struct DataAccount {
    pub random_number: u32
}
```

**Syntax**

struct

- 提示
    
    ```rust
    #[account]
    pub struct MyAccount {
        pub data: u32,
    }
    ```