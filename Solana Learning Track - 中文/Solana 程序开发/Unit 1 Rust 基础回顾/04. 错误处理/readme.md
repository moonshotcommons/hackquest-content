# Content

学习目标：掌握 Rust 的 Result 返回值类型，以及 Solana 中的 Program 类型。

我们在 Rust 基础课程《6.1 错误处理》中介绍了 Result 类型，这里我们简单回顾下。

### Result 枚举

`Result`是一个标准库类型，表示两种不同的情况：成功 ( `Ok` ) 或失败 ( `Err` )。当您使用 Ok 或 Err 时，必须包含一个值，该值的类型由代码的上下文确定。例如，定义返回值类型为`Result<String, i64>`的函数则表示该函数可以返回带有`String`的 Ok 或带有`i64`整数的 Err 。在此示例中，整数是可用于适当处理错误的错误代码。

要返回带有 String 的成功案例，您可以执行以下操作：

```jsx
Ok(String::from("Success!"));
```

要返回整数错误，您可以执行以下操作：

```jsx
Err(404);
```

### ProgramResult 枚举

`ProgramResult`是 solana 中定义的一个通用错误处理类型，它是`solana_program`中的一个结构体，具体如下：

```jsx
use solana_program::entrypoint::ProgramResult;
```

代表着 Solana 程序中指令处理函数的返回值，该类型代表 Transaction 交易中指令的处理结果，成功时为单元类型`()`，即返回值为空，失败时返回值为`ProgramError`，它本身又是个枚举。

```jsx
use std::result::Result as ResultGeneric;

pub type ProgramResult = ResultGeneric<(), ProgramError>;
```

在 ProgramError 中定义了 23 种常见的错误原因枚举值，也支持自定义的错误类型，如下：

```jsx
pub enum ProgramError {
    // 用户自定义错误类型
    #[error("Custom program error: {0:#x}")]
    Custom(u32),

		// 参数无效
    #[error("The arguments provided to a program instruction were invalid")]
    InvalidArgument,

		// 指令数据无效
    #[error("An instruction's data contents was invalid")]
    InvalidInstructionData,

		// 账户数据无效
    #[error("An account's data contents was invalid")]
    InvalidAccountData,
    
		// ……
}
```