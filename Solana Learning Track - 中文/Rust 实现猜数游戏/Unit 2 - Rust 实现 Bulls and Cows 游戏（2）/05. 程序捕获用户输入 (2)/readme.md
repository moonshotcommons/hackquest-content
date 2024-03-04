# Content/**捕获用户输入**

经过上一节课的学习，我们知道了如何引入 ***std::io*** 模块，为接下来程序捕获用户输入的数字做好了准备。现在，我们就开始学习，如何使用这个 ***io*** 模块来读取用户在终端输入的数字。

### **创建用于存储用户输入的变量**

为了存储用户输入的数据，我们需要一个变量。这个变量应该是可变变量，因为用户可以多次输入，导致变量可以随时改变。

```rust
let mut input_data = String::new();
```

- ***String::new()*** ：创建一个新的空字符串，作为用户输入数据的存储容器。
- ***let mut input_data***：声明了一个名为 ***input_data*** 的可变字符串变量，并初始化为 ***String::new()***  空字符串。

### **读取用户输入**

接下来，我们使用 ***std::io*** 模块中的 ***stdin*** 函数来读取用户的输入。

```rust
io::stdin().read_line(&mut input_data);
```

- ***io::stdin()***：用于获取用户在终端的输入。它提供了一个通道，允许程序接收用户通过键盘输入的数据。简单来说，它就像是连接用户键盘和你的程序的桥梁。
- ***read_line(&mut input_data)***：用来读取用户输入的文本并将其存储到指定的变量中。这个方法需要一个变量的可变引用，以便它可以将捕获的输入保存到那个变量里。

简单来说，这行代码使用 ***stdin()*** 函数获取终端输入的句柄，并调用 ***read_line*** 方法将用户输入的数据写入之前创建的 ***input_data*** 字符串。

**Syntax**

Mutable Variable

String

Function Call

- 提示
    
    ```rust
    let mut number = 1;
    let mut str = String::new();
    rand::thread_rng().gen_range(1..11);
    ```