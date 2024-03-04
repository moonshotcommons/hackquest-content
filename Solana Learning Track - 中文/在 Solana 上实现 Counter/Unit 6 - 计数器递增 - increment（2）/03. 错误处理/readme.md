# Content/错误处理

接着上一节的内容，我们在使用 `require_keys_eq!` 宏进行权限验证时，如果公钥不匹配会返回错误代码，接下来，我们就来具体看如何定义错误。

### **错误码枚举（ErrorCode Enum）**

在程序中，错误处理是一个重要的部分。`ErrorCode` 枚举允许我们定义一系列可能的错误情况，并为每种错误指定一个清晰的消息。

### 定义 ErrorCode 枚举

1. **使用** `#[error_code]` **属性**：
    
    `#[error_code]` 是一个属性，用于标记 `ErrorCode` 是一个用于定义错误代码的枚举。这个属性使得 `ErrorCode` 的每个变量都与一个特定的错误情况相关联。
    
2. **定义不同的错误类型**：
    
    在 `ErrorCode` 枚举中，我们可以定义多种不同的错误类型。每种类型都代表了程序执行过程中可能遇到的一个具体错误。
    

```rust
#[error_code]
pub enum ErrorCode {
    #[msg("The requested operation is not permitted.")]
    OperationNotAllowed,

    #[msg("The provided input is invalid.")]
    InvalidInput,

    #[msg("Insufficient funds to perform the operation.")]
    InsufficientFunds,

    // 更多错误类型...
}
```

这里：

- `#[msg("...")]`: 每个错误类型前的属性用于定义当该错误被触发时返回给用户的具体错误消息。
- 枚举的变量: 如 ***OperationNotAllowed***、***InvalidInput*** 和 ***InsufficientFunds***，这些是自定义的错误类型，可以根据程序的具体需求来定义。

因此，我们需要定义一个未授权的错误类型在 `require_keys_eq!`  宏进行权限判断时中使用。

**Syntax**

ErrorCode 

- 提示
    
    ```rust
    #[error_code]
    pub enum ErrorCode {
        #[msg(".....")]
        Unauthorized,
    }
    ```