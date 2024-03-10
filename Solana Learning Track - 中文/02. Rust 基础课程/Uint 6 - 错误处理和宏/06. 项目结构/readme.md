# Content/概念

**`module`**：用于组织和封装代码的单元。它可以包含函数、结构体、枚举、常量、Trait等，也可以包含其他模块。通过使用`mod`关键字可以在 Rust 中创建模块，并且模块可以嵌套形成模块树。

**`crate`：**是 Rust 中的编译单元，可以是**库 crate** 或**二进制 crate**（它们的区别参见FAQ）。一个 crate 可以包含一个或多个模块。

**`package`：**是一个包含一个或多个相关 crate 的项目工程。它由一个 `Cargo.toml`文件定义，该文件包含有关项目的元信息、依赖关系以及其他配置选项。一个 package 可能包含一个主 crate（通常是可执行文件）和零个或多个库 crate（通常是依赖 crate）。

- 比喻
    
    我们把 Package（项目）类比为整个房子，房子的整体规划和设计类似于项目的`Cargo.toml`文件，它定义了项目的元信息和整体结构。整个房子由许多组件（crate）组成，例如厨房、卧室、客厅等。每个房间有各自的家具及功能，比如沙发、床、做饭，就像 module 中的结构体、枚举、函数等。
    
- 真实用例
    
    Rust 中的`crate`包含了在多个项目中可以共享的`module`，如果我们要访问某个 module 中的项（如函数、结构体、枚举、Trait、常量等），我们需要知道它的路径（就像文件系统中的导航那样）。到某个特定module或者项的路径，其实是由 crate 中每一步的名称以`::`分隔组成的。我们看下面的结构：
    1、根 crate 是 `solana_program`
    
    2、`solana_program`包含了一个名为`account_info`的模块
    
    3、`account_info`模块包含了`AccountInfo`
    
    因此`AccountInfo`的路径就是`solana_program::account_info::AccountInfo`，我们需要在代码中指定整个路径才能使用它，但是每次都写上完整的路径未免太繁琐。因此，可以使用`use`关键字将其引入到作用域中，这样每次使用时就不用带上完整的路径，
    如`use solana_program::account_info::AccountInfo`。
    

### Documentation

下面的代码分别展示了模块（module）的定义。

```solidity
// mod 定义一个模块，后面跟着模块名（my_module）
mod my_module {
    // 模块的内容
    pub fn my_function() {
        // 函数体
    }
}
```

### FAQ

**Q：请详细介绍 Rust 中 库 crate 和二进制 crate 的概念？**

A：库 crate 和二进制 crate 是两种不同类型的 Rust 项目。它们分别用于构建库（用于被其他程序引用）和可执行程序。我们分别看下它们的概念及区别：

**库 crate** ：是一种 Rust 项目，通过`cargo new --lib 库名`来创建，它的主要目的是提供可供其他程序引用的功能性代码。库 crate 的代码通常是一些通用的、可复用的功能。

组织方式： 一个库 crate 的代码通常位于一个名为`lib.rs`的文件中，该文件包含 crate 的主模块。库 crate 的代码可以由其他 crate 引用，通过在 Cargo.toml 文件中添加相应的依赖。

**二进制 crate**：也是一种 Rust 项目，通过`cargo new 项目名`来创建，它的主要目的是构建可执行程序。这个 crate 可以包含多个模块，其中一个模块被指定为主入口点，例如 `main.rs` 文件。二进制 crate 的代码用于创建独立的可执行文件。

组织方式： 一个二进制 crate 的代码通常包含在一个名为 `main.rs` 的文件中，该文件包含程序的主函数 `main()`。

总的来说，库 crate，用于构建可供其他程序引用的功能性代码；代码通常位于 `lib.rs` 文件中；可以被其他 crate 引用作为依赖。而二进制 crate，用于构建可执行程序；代码通常位于 `main.rs` 文件中；产生一个独立的可执行文件。

**注意：** 在一个 Rust 项目中，你可以同时包含库 crate 和二进制 crate。例如，一个项目可能包含一个库用于提供通用功能，同时也包含一个可执行程序用于演示或测试该库。在这种情况下，项目的目录结构通常包含 `src/lib.rs` 和 `src/main.rs`。

# Example/示例代码

下面的例子演示了模块（module）的层次结构，构建了一个 crate，最终组成了一个 package。通过模块的层次组织，代码具有良好的结构和可读性。

```rust
// src/main.rs

// 主模块，相当于房子的大厅
mod living_room {
    // 子模块，相当于房子的卧室
    mod bedroom {
        // 模块中的函数，相当于卧室中的家具
        pub fn sleep() {
            println!("Sleeping in the bedroom");
        }
    }

    // 子模块，相当于房子的厨房
    mod kitchen {
        // 模块中的函数，相当于厨房中的设备
        pub fn cook() {
            println!("Cooking in the kitchen");
        }
    }

    // 主模块中的函数，相当于大厅中的活动
    pub fn relax() {
        println!("Relaxing in the living room");
        bedroom::sleep(); // 调用卧室模块中的函数
        kitchen::cook();  // 调用厨房模块中的函数
    }
}

// 主函数，相当于整个房子的入口
fn main() {
    // 调用 living_room 模块中的函数
    living_room::relax();
}
```