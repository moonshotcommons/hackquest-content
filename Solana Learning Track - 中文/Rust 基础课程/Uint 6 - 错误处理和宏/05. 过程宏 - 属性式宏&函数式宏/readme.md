# Content/概念

在前几节的基础上，我们继续学习***属性式宏***和***函数式宏***。

说明：也有人将其称为 ***类属性宏*** 和 ***类函数宏***，但这里提到的“类”并不是面向对象编程中的`class`，而是`like`，类似于的意思，因此这种叫法很容易让人混淆，翻译成“属性式”和“函数式”则更加贴切。

**属性式宏**（attribute-like macro）：定义了可添加到标记对象的新外部属性。这种宏通过`#[attr]`或`#[attr(…)]`方式调用，其中`…`是标记的具体属性（可选）。

一个属性式宏定义的简单框架如下所示：

```jsx
use proc_macro::TokenStream;

// 这里标记宏的类型
#[proc_macro_attribute]
pub fn custom_attribute(input: TokenStream, annotated_item: TokenStream) -> TokenStream {
    annotated_item
}
```

这里需要注意的是，与派生宏、函数式宏不同，属性式宏有两个输入参数，而不是一个。

- 第一个参数是属性名称后面的带分隔符的标记项（即`#[attr(…)]`中`(…)`的具体内容）。如果只有属性名称（其后不带标记项，比如 `#[attr]`），则这个参数的值为空。
- 第二个参数是标记的代码项本身的 Token 流，它可以是被标记的字段、结构体、函数等（见真实用例）。

- 比喻
- 真实用例
    
    如下是 Solana 中 anchor 框架用到的`#[account(..)]`属性式宏，它按照该宏配置的属性来初始化 PDA 账户，其中`init`、`seeds`、`payer`等属性作为宏定义中第一个 TokenStream 参数，而`pub pda_counter: Account<'info, Counter>,` 作为宏定义中第二个 TokenStream 参数。而对于结构体`Counter`，则使用`#[account]`进行标记，以便 anchor 框架自动实现结构体的反序列化。
    
    ```rust
    pub struct InitializeAccounts<'info> {
    
    	#[account(init, seeds = [b"my_seed", user.key.to_bytes().as_ref()], payer = user, space = 8 + 8)]
    	pub pda_counter: Account<'info, Counter>,
    	// ……
    }
    
    #[account]
    struct Counter {
    	count: i32,
    }
    ```
    

### Documentation

如下的代码展示了一些常见的属性式宏：`#[cfg(…)]`是根据条件编译的属性宏、`#[test]`是用于标记测试函数的属性宏、`#[allow(...)]`和 ****#`[warn(...)]`控制编译器的警告级别。

```solidity
// 用于根据条件选择性地包含或排除代码
#[cfg(feature = "some_feature")]
fn conditional_function() {
    // 仅在特定特性启用时才编译此函数
}

#[test]
fn my_test() {
    // 测试函数
}

#[allow(unused_variables)]
fn unused_variable() {
    // 允许未使用的变量
}
```

### FAQ

**Q：什么是函数式宏（function-like macro）？**

A：函数式宏跟声明宏类似，采用`macro_rules!`关键字定义，通过`custom_fn_macro!(…)`的方式来调用。但不同于声明式宏使用模式匹配的方式，函数宏则更像是常规的函数调用，可以使用各种 Rust 语法，包括条件语句、循环、模式匹配等，使得它更加灵活和强大。

函数式的定义简单编写框架如下所示：

```jsx
use proc_macro::TokenStream;

// 这里标记宏的类型
#[proc_macro]
pub fn custom_fn_macro(input: TokenStream) -> TokenStream {
    input
}
```

可以看到，这实际上只是从一个`TokenStream`到另一个`TokenStream`的映射，其中 input 是调用分隔符内的标记项。

例如，对于示例调用`foo!(bar)`，input 输入标记流即为`bar`。返回的标记流将替换宏调用。

右侧我们展示了 Rust 中常见的函数式宏，以及 Solana 中anchor 框架的`declare_id!`宏

# Example/示例代码

这里展示了常见的函数式宏。

```solidity
// vec! 用于创建Vec的宏。
let my_vector = vec![1, 2, 3];

// println! 和 format! 用于格式化字符串的宏。
let name = "World";
println!("Hello, {}!", name);

let formatted_string = format!("Hello, {}!", name);

// assert! 和 assert_eq! 用于编写断言的宏。
assert!(true);
assert_eq!(2 + 2, 4);

// panic! 用于在程序中引发Panic异常的宏。
panic!("Something went wrong!");

// env! 用于在编译时获取环境变量的宏。
let current_user = env!("USER");
println!("Current user: {}", current_user);

// declare_id! 是 anchor 框架中用于声明程序ID的宏
declare_id!("3Vg9yrVTKRjKL9QaBWsZq4w7UsePHAttuZDbrZK3G5pf");
```