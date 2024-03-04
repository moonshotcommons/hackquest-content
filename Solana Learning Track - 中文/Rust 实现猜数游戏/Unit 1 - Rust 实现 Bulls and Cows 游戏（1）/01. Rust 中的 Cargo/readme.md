# Content/Cargo 是什么

Cargo 是 Rust 编程语言的包管理器和系统构建工具。就像你建造一座大楼需要工具和材料一样，Cargo 提供了你在 Rust 项目开发中所需的所有工具和库。

Cargo 能帮助你从创建项目、下载项目依赖、编译代码、构建和测试、直至最后运行和部署你的项目，就像一个贴心的小助手，确保一切都井井有条地运行起来。

### 如何安装 Cargo

- 如果我们之前已经安装好 Rust ，就会一并安装 Cargo，无需额外再安装；
- 如果还未安装过 Rust 环境，可以参考以下教程进行安装： **[安装 Rust](https://course.rs/first-try/installation.html#%E5%AE%89%E8%A3%85-rust)** 或 ****[Rust Install](https://www.rust-lang.org/tools/install)

无论你是初学者还是资深开发者，Cargo 都将是你在 Rust 开发中不可或缺的工具。当然，如果不熟悉也不要紧，接下来，让我们一起学习 Cargo 的相关指令。

### Cargo 相关指令

下面是一些基础的 Cargo 指令：

```bash
cargo new (project's name)  //创建一个新的 cargo 项目
cargo build                 //编译项目
cargo run                   //对项目进行编译，然后再运行
```

- 其他指令
    
    我们可以在命令行工具运行`cargo -h` 指令，查看 Cargo 的所有指令以及相关介绍：
    
    ```jsx
    		clean       Remove the target directory
        doc, d      Build this package's and its dependencies' documentation
        new         Create a new cargo package
        init        Create a new cargo package in an existing directory
        add         Add dependencies to a manifest file
        remove      Remove dependencies from a manifest file
        run, r      Run a binary or example of the local package
        test, t     Run the tests
        bench       Run the benchmarks
        update      Update dependencies listed in Cargo.lock
        search      Search registry for crates
        publish     Package and upload this package to the registry
        install     Install a Rust binary. Default location is $HOME/.cargo/bin
        uninstall   Uninstall a Rust binary
    ```