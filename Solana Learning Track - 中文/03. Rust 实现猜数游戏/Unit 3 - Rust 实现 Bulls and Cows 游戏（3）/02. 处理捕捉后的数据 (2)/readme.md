# Content/**转换和处理用户输入**

在上一节课中，我们学习了如何使用 trim 方法去除用户输入中的不必要空白字符。接下来的这节课，我们将学习如何将把字符串转换成数值类型，并对转换的结果进行处理，以便后续的逻辑判断和计算。

### **使用 parse 转换字符串**

上一节课，我们使用 `trim` 处理输入的字符串。

```rust
let guess = guess.trim()；
```

我们再调用 `parse` 方法，并指定转换后的类型。在这个例子中，我们将尝试将字符串转换为 `u32` 类型的整数：

```rust
let guess: u32 = match guess.trim().parse() {
					
		Ok(num) => num,
		Err(_) => {
		    println!("Please input valid number");
		    continue;
		}
};
```

- ***let guess: u32 = match guess.trim().parse() { ... }***：这行代码尝试将去除空白符后的字符串解析为 `u32` 类型的整数，因此，我们把原来的 ***guess*** 变量声明为 `u32` 整数类型。
- ***match*** ：`parse` 方法转换字符串为整数类型时，可能成功、也可能失败，所以，我们使用 `match` 表达式允许我们处理每种可能的结果（**`Ok`** 和 **`Err`**）并返回。
- ***Ok(num) => num***：如果 `parse` 成功，**Result** 将会是 ***Ok(num)***，其中 ***num*** 是解析得到的数值。此处，我们使用 `=>` 将得到的整数 ***num*** 直接返回。
- ***Err(_) => {...}***：如果 `parse` 失败，**Result** 会是 ***Err(_)***，其中 `_` 是一个通配符，表示我们不关心具体的错误信息。这里我们输出一条错误消息，并使用 `continue` 跳过本次循环，提示用户重新输入。

**Syntax**

String parse

match

Result

- 提示
    
    ```rust
    let number: u32 = match text.trim().parse() {
    					
    		Ok(num) => num,
    		Err(_) => {
    		    println!("Please input valid number");
    		    continue;
    		}
    };
    ```