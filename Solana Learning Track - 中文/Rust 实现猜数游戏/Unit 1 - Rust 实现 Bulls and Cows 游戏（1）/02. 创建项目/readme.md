# Content/创建项目

在上一课中，我们了解了 Rust 的包管理器和构建工具 Cargo，包括一些基础指令：创建项目、编译和运行项目。现在，我们将正式学习如何使用 Cargo 来创建你的第一个 Rust 项目 - ***Bulls and Cows***。

<aside>
💡 确保你已经按照上一课的指引安装了 Rust 和 Cargo，它们是你在接下来的 Rust 项目实战中不可或缺的工具。

</aside>

### **具体步骤**

1. 打开我们的命令行工具
    
    这是开始任何 Rust 项目的第一步。无论你是 **Windows**、**Linux** 还是 **macOS** 用户，找到并打开你的命令行工具。
    
2. 输入创建项目指令
    
    在你的终端中输入以下命令来创建一个新的 Rust 项目 - ***Bulls and Cows***：
    
    ```bash
    cargo new bulls_and_cows
    ```
    
    > 在 Rust 中，项目名通常使用**小写字母**，并用**下划线**代替**空格**来保持一致性和兼容性。因此，描述性名称 ***Bulls and Cows*** 在实际创建时会转换为 ***bulls_and_cows***。
    > 
3. 进入项目目录
    
    创建项目后，使用以下命令进入项目目录：
    
    ```bash
    cd bulls_and_cows
    ```
    

### 目录结构

创建完项目 ***Bulls and Cows*** 后，我们进入 ***bulls_and_cows*** 文件夹， 可以看到 Cargo 自动生成的文件和目录：

```bash
$ tree
.
├── .git
├── .gitignore
├── Cargo.toml
└── src
    └── main.rs
```