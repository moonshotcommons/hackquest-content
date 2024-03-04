# Content/**处理输入异常**

经过上一节课的学习，我们学会了如何读取用户输入的数据，但这个方法可能返回错误的信息，因此，这节课我们就将学习如何处理输入的错误。

### **理解** *read_line* **的返回值**

```rust
io::stdin().read_line(&mut guess);
```

上节课我们学习了如何通过 ***io.stdin()*** 中的 ***read_line()*** 方法读取用户在命令行输入的值。

> ***read_line()*** 方法在读取输入时可能会遇到各种问题，例如，用户输入非法字符或输入过程中发生中断等。
> 

 ***read_line()*** 方法会返回一个 ***Result*** 类型的值，这是一个枚举，其值可以是 ***Ok*** 或 ***Err***。

- **Ok**：表示操作成功，包含成功读取的字节数。
- **Err**：表示操作失败，包含错误信息。

### **使用** expect **处理错误**

为了处理可能发生的错误，我们使用 ***expect*** 方法。如果 ***read_line*** 方法返回一个 ***Err*** 值，expect 将会停止程序并显示你提供的错误信息，它可以帮助你快速发现并处理错误。

```rust
io::stdin().read_line(&mut guess).expect("Failed to read line");
```

在 ***read_line*** 调用后添加 `.expect("Failed to read line")`。这样，如果读取输入时出现错误，程序会停止运行，并显示 *"Failed to read line"*。

**Syntax**

**Error Handling with expect**

- 提示
    
    ```rust
    .expect("error message");
    ```