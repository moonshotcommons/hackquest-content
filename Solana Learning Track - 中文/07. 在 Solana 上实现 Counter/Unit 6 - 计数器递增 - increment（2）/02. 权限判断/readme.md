# Content/权限判断

在上一节中，我们已经成功地定义了 ***increment*** 函数的头部，并明确了函数的访问性和返回类型。现在，我们将着手实现函数内部的关键逻辑，首先是权限判断。

### **实现权限判断**

1. **使用** `require_keys_eq!` **宏进行比较**：
    
    在函数的开始部分，我们首先需要确保调用此函数的用户具有适当的权限。为此，我们可以使用 `require_keys_eq!` 宏。这个宏将帮助我们验证调用者是否为授权用户。
    
    <aside>
    💡 `require_keys_eq!` 宏比较两个公钥参数。如果这两个公钥相等，宏不做任何事情，程序继续执行。如果不相等，它会触发一个错误。
    
    </aside>
    
2. **处理权限验证失败的情况**：
    
    如果宏中比较的两个公钥不匹配，意味着执行操作的用户没有适当的权限，我们需要通知调用者。在这种情况下，我们返回 `ErrorCode::Unauthorized` 错误。（这个错误我们在下一节中会详细说明）
    

```rust
require_keys_eq!(key1, key2, error_code);
```

这样的错误处理确保了只有正确授权的用户才能更改计数器的值，增强了链上程序的安全性。

**Syntax**

require_keys_eq!

- 提示
    
    ```rust
    require_keys_eq!(
        ctx.accounts.authority.key(),
        ctx.accounts.counter.authority,
        ErrorCode::Unauthorized
    );
    ```