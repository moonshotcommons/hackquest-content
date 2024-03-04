# Content/获取时间戳

在上一节课中，我们已经通过 Solana 程序库获取当前时间戳并生成了随机数，这节课，我们将继续对这个随机数进行处理。

**处理随机数**

为了确保随机数不为 0，范围在 1～10 之间，我们将得到的这个数字加 *1*：

```rust
fn generate_random_number() -> u32 {
     let c = Clock::get().expect("Failed to get clock");
     let last_digit = (clock.unix_timestamp % 10) as u8;
     let random_number = (last_digit + 1) as u32;
     random_number
}
```

将其转换为 `u32` 类型并返回。这样我们就得到了一个 **1到10** 之间的随机数字。

**Syntax**

**%**：取模运算。

**as**：类型转换

- 提示
    
    ```rust
    let random_number = (number + 1) as u32;
    ```