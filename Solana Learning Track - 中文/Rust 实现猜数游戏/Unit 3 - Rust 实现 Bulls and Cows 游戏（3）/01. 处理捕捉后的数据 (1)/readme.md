# Content/**数据预处理**

在之前的课程中，我们学习了如何捕获用户输入的数据。接下来，我们将学习如何对这些捕获的数据进行预处理，以确保数据的准确性和可用性。

这一节，我们将使用 trim 方法去除用户输入中不必要的空白字符。

### **去除空白字符**

当用户输入数据时，他们可能会在开始或结束时不小心加入空格或换行符。这些额外的空白字符可能会干扰我们程序的逻辑判断。因此，我们使用 trim 方法来清除这些不需要的字符。

```rust
let input_data = "   42   ";
let trimmed_data = input_data.trim();

println!("Original Data: '{}'", input_data); //"   42   "
println!("Trimmed Data: '{}'", trimmed_data);//"42";
```

这行代码去除了 ***input_data*** 字符串两端的所有空白字符，并将结果存储在新的变量 ***trimmed_data*** 中。

**Syntax**

String

trim

- 提示
    
    ```rust
    let trimmed = text.trim();
    ```