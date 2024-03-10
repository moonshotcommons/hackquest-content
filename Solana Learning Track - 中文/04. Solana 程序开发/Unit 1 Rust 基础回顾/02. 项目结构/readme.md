# Content

学习目标：回顾 Rust 的项目结构以及依赖引入。

我们在 6.6章节《Rust的项目结构》中介绍了module、crate、package的概念，这里我们简单回顾下：

**`module`**：用于组织和封装代码的单元。它可以包含函数、结构体、枚举、常量、Trait等，也可以包含其他模块。通过使用`mod`关键字可以在 Rust 中创建模块，并且模块可以嵌套形成模块树。

**`crate`：**是 Rust 中的编译单元，可以是**库 crate** 或**二进制 crate**，一个 crate 可以包含一个或多个模块。

**`package`：**是一个包含一个或多个相关 crate 的项目工程。它由一个 `Cargo.toml`文件定义，该文件包含有关项目的元信息、依赖关系以及其他配置选项。

简单来说，module 是 crate 的子集，而crate 是 package 的子集，在本节中，我们将重点关注 module 和 crate 的使用。

### 引入依赖

Rust 中的`crate`包含了一些通用的`module`。如果我们想访问 module 中的某个`item`（它可能是函数、结构体、Trait等），那么我们需要知道它的“路径”（就像我们在文件系统中导航时一样）。

将 crate 结构视为一棵树，其中 crate 是基础，module 是分支，每个分支都可以具有作为附加分支的子模块或项目 item。

特定模块或项目的路径是从 crate 到该模块的每个步骤的名称，其中每个步骤均由`::`分隔。作为示例，让我们看一下以下结构：

- 基础的 crate 是 solana_program
- solana_program 包含一个名为 account_info 的 module
- account_info 包含一个名为 AccountInfo 的结构

那么`AccountInfo`的路径为`solana_program::account_info::AccountInfo`。

如果没有任何其他关键字，我们需要引用整个路径才能在代码中使用AccountInfo 。

但是，使用**`use`**关键字，我们可以将某个 item 纳入范围，以便可以在整个文件中重复使用它，而无需每次都指定完整路径。在 Rust 文件的顶部经常会看到一系列use命令。就像这样

```jsx
use solana_program::account_info::AccountInfo
```