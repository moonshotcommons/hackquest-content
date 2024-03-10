# Content/获取当前区块链状态下的时间信息

上一节课我们已经成功导入了 Solana 程序库的 ***Clock*** 模块，这节课，我们将利用它来获取当前的时间信息，这样在后面的课程，我们就可以根据这个时间来生成一个随机数。

现在，我们就可以使用我们上节课导入的 ***Clock*** 模块，获取到当前区块链状态下的时间信息：

```rust
fn generate_number() -> u32 {
	let clock = Clock::get().expect("Failed");	
}
```

- `Clock::get()`：我们调用 `Clock::get()` 来获取到 ***Clock*** 实例；
- `expect("Failed")`：如果无法获取到，程序将会停止，并显示 *"Failed"*。

**Syntax**

function call

- 提示
    
    ```rust
    fn generate_number() -> u32 {
    	let clock = Clock::get().expect("Failed");	
    }
    ```