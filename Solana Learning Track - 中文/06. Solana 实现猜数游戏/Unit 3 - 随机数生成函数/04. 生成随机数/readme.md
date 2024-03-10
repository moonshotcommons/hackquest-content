# Content/获取时间戳

在上一节课中，我们已经通过 Solana 程序库获取到了当前区块链状态下的时间信息，现在，我们将继续学习如何使用它来生成一个简单的随机数。

**获取当前时间戳的最后一位数字**

我们将使用这个 ***Clock*** 实例获取代表当前时间的时间戳，然后取时间戳的最后一位数字来代表我们生成的随机数：

```rust
fn generate_random_number() -> u32 {
	let c = Clock::get().expect("Failed to get clock");
	let last_digit = (c.unix_timestamp % 10) as u8;
}
```

我们通过对时间戳取模（`%10`）来获取当前时间戳的最后一位数字，作为随机数，然后将其转换为 `u8` ****类型。

- `unix_timestamp`： UNIX 时间戳。

**Syntax**

**%**：取模运算。

- 提示
    
    ```rust
    let last_digit = (clock.unix_timestamp % 10) as u8;
    ```