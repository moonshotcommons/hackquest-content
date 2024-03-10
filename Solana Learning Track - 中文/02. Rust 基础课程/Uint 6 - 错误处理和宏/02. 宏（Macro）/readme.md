# Content/概念

**学习目标**：本节我们先从**整体**上学习宏的基础概念，并认识几个 Rust 中常见的宏。

`**宏（Macro）**`是一种**元编程**（metaprogramming）的工具，使得开发者能够编写能够生成代码的代码，从而提高代码的灵活性和重用性。更详尽的解释可以参见本课的 FAQ。Rust 中的宏分为以下两种类型：

**声明式宏**（Declarative Macros）允许开发者使用宏规则（`macro_rules!`）创建模式匹配和替换规则，根据匹配到的模式进行代码替换。声明式宏是一种基于文本的宏，它仅仅是简单的文本替换，并没有对语法树进行操作。

**过程宏**（Procedural Macros）允许开发者在代码生成阶段使用 Rust 代码来处理输入并生成输出。而非像声明式宏那样匹配对应模式然后以另一部分代码替换当前代码，因此是更为强大和灵活的宏形式，过程宏有三种主要类型：派生宏（`derive macros`）、属性式宏（`attribute-like macros`）和函数式宏（`function-like macros`）。

总体而言，声明式宏主要是基于简单的文本替换和模式匹配，适用于对代码进行简单的转换。过程宏则更为灵活，允许在编译期间生成和操作 AST，提供了更丰富的功能，但相对复杂一些，需要更深入的理解和使用。选择声明式宏还是过程宏通常取决于所需功能的复杂性和类型安全的要求。

> AST（Abstract Syntax Tree，抽象语法树）：Rust 源代码在编译器中会被解析成词法单元（Token），并进一步解析成一种树状结构，其中的每个节点表示源代码的一个语法结构元素，比如表达式、语句、函数声明等。节点之间通过树状结构相互连接，反映了源代码中的嵌套和层次关系。
> 

- 比喻
    
    可以将 Rust 中的宏比作“***代码的模板***”或者“***代码的生成器***”。让我们通过一个生活中的类比来更好地理解宏的概念：想象一下你经营着一家商品定制工厂。你的客户希望订购一些特定规格和样式的产品，但每个人的需求都可能不同。你可以设计一些通用的产品模板，然后根据客户的需求，使用这些模板生成定制的商品。这些模板就类似于 Rust 中的宏。它包含了一些通用的结构和规则，但具体的细节取决于客户的定制需求。
    
- 真实用例
    
    `solana`的程序中使用了多个宏来简化程序的开发流程，同时提高代码的可读性和可维护性，使开发者可以更加专注于业务逻辑的实现，而无需过多关注与 Solana 账户和交互相关的底层细节。
    
    ```rust
    // 类属性宏：用于设置 Solana 程序ID
    declare_id!("3Vg9yrVTKRjKL9QaBWsZq4w7UsePHAttuZDbrZK3G5pf");
    
    // 派生宏：用于（反）序列化
    #[derive(BorshSerialize, BorshDeserialize)]
    struct NoteState {
        title: String,
        body: String,
        id: u64
    }
    ```
    

### Documentation

这里展示了 Rust 中最常见的一些宏：

```solidity
// 日志打印宏 println!
println!("hello, micro");

// 动态数组创建宏 vec!
let _dyc_arr = vec![1, 2, 3];

// 断言宏 assert!，判断条件是否满足
let x = 1;
let y = 2;
assert!(x + y == 3, "x + y should equal 3");

// 格式化字符串的宏 format!
let name = "world";
let _message = format!("Hello, {}!", name);
```

### FAQ

**Q：Rust 中宏和函数究竟有什么区别？**

A：在 Rust 中，宏和函数都是用于代码重用的工具，但它们之间有一些重要的区别。

首先，宏是一种**编译时**工具，而函数是一种**运行时**工具。这意味着，宏在编译时被展开并生成代码，而函数则在程序运行时被调用并执行代码。因此，使用宏可以在编译时进行更多的优化和检查，从而提高程序的性能和安全性。

其次，宏可以接受任意数量和类型的参数，并且可以在编译时生成任意类型的代码。这使得宏非常灵活，可以用于各种不同的场景。例如，宏可以用于生成数据结构、定义域特定语言、实现代码模板等等。

另外，宏还可以使用 Rust 的元编程功能，例如宏定义中的 `#[derive]` 属性可以自动生成代码，这在某些情况下可以减少编写代码的工作量。

下面是一个简单的示例，展示了如何使用宏和函数来实现相同的功能。假设我们要编写一个函数，将一个字符串转换为大写字母：

```rust
fn to_upper_case(s: &str) -> String {
    s.to_uppercase()
}

fn main() {
    let s = "hello, world!";
    let result = to_upper_case(s);
    println!("{}", result);
}

```

这个函数很简单，但是我们可以使用宏来实现同样的功能，如下所示：

```rust
macro_rules! to_upper_case {
    ($s:expr) => {
        $s.to_uppercase()
    };
}

fn main() {
    let s = "hello, world!";
    let result = to_upper_case!(s);
    println!("{}", result);
}

```

这个宏看起来比函数更复杂，但它的优点也很明显：***可以在编译时展开，这使得宏在编译时进行更多的优化和检查，从而提高程序的性能和安全性***。在上面的例子中，宏展开后，在生成的代码中直接使用`to_uppercase`方法，而不需要调用`to_upper_case`函数，减少了程序的运行时间和内存使用。Rust 编译器将将宏展开为以下代码：

```rust
let s = "hello, world!";
let result = s.to_uppercase();
println!("{}", result);
```

总之，宏和函数都是 Rust 中非常有用的工具，需要根据具体的需求选择使用哪种方式。

# Example/示例代码

这里我们创建了一个简单的声明式宏`double!`，进行简单的文本替换。

```solidity
// 宏规则
macro_rules! double {
    ($x:expr) => {
		// 替换代码，将表达式加倍
        $x * 2
    };
}

fn main() {
    let result = double!(5);
    println!("Result: {}", result); // 输出：Result: 10
}
```