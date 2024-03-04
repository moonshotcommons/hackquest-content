# Content/概念

**学习目标**：了解声明式宏的实现逻辑及应用。

通过前面的学习，我们对 Rust 中的宏有了初步认识，本节我们继续学习其中的声明式宏，首先回顾下它的概念：

**声明式宏**（Declarative Macros）采用了类似`match`的机制（见4.2节模式匹配），允许开发者使用宏规则`macro_rules!`创建***模式匹配和替换规则，根据匹配到的模式进行代码替换***。声明式宏是一种基于文本的宏，它仅仅是简单的文本替换，并没有对语法树进行操作。

> 语法树是代码的抽象表示，它以树状结构表示代码的语法结构。在宏中，语法树是由一个个代码单元组成的抽象结构，用于表示代码的语法和结构。宏可以通过操作语法树来生成、修改或重组代码。
> 

- 比喻
- 真实用例
    
    `entrypoint!`宏是 solana 程序中一个特殊的宏，它用于声明程序入口点并设置全局处理程序*。*
    
    ```rust
    // 声明式宏：用于声明 solana 程序入口点函数
    entrypoint!(process_instruction);
    
    // 处理指令的逻辑
    pub fn process_instruction(
        program_id: &Pubkey, 
        accounts: &[AccountInfo],
        _instruction_data: &[u8],
    ) -> ProgramResult {
    		Ok(())
    }
    ```
    

### Documentation

这里展示了一个简单的声明式宏的定义（使用关键字`macro_rules!`），该宏通过参数个数实现了2种模式匹配机制。

*注意：Rust 编译器对该宏展开后，并不是对2个数进行了求和计算，而是将其展开为2个相加的数字，代码如下：*

```solidity
// 宏的定义
macro_rules! add {
		// 匹配 2 个参数，如add!(1,2), add!(2,3)
    ($a:expr,$b:expr) => {
        // macro 宏展开的代码
        {
            // 表达式相加
            $a + $b
        }
    };

		// 匹配 1 个参数，如 add!(1), add!(2)
    ($a:expr) => {{
        $a
    }};
}

fn main() {
		let x = 0;
    // 宏的使用
    add!(1, 2);
    add!(x);
}

// 宏展开的代码如下
fn main() {
	{
		1 + 2
	}
}
```

### FAQ

**Q1：Rust 宏中的 Token 是什么概念？**

A：Token 是 Rust 代码的最小单元，它是源代码中的一个元素，代表了语法的一部分。在 Rust 中，Token可以是关键字、标识符、运算符、符号等。在宏中，我们需要操作和理解这些 Token，以便生成或转换代码。

```rust
macro_rules! add {
    ($a:expr,$b:expr) => {{
        $a + $b
    }};
}
```

上面的代码中，参数以`$`作为开头，`**:**`后表明该参数的类型，参数类型通常被称为`Token`，Rust 中常见的 Token 类型有：

- 表达式（`expr`）：表示 Rust 代码中的表达式，例如 `x + y`、`if condition { true } else { false }` 等，数字也是一种表达式。
- 语句（`stmt`）：表示 Rust 代码中的语句，例如 `let x = 1;`、`println!("Hello, world!");` 等。
- 类型（`ty`）：表示 Rust 代码中的类型，例如 `i32`、`bool`、`String` 等。
- 标识符（`ident`）：表示 Rust 代码中的标识符，例如变量名、函数名、结构体名等。
- 通用 Token（`tt`）：表示 Rust 代码中的任意 Token，可以用于匹配和生成任意类型的 Token。

**Q2：声明式宏如何实现比函数更加灵活的功能，如不确定的参数类型、非固定数量的参数等？**

A：通过 Q1 我们知道，可以使用标记类型为`ty` 的参数作为数据类型，如 `u8`、`u16` 等。我们接着改下上面的代码，使得该宏在添加数字之前，将其转换为特定类型。

```rust
macro_rules! add_as {
    // ty 表示参数类型
    ($a:expr,$b:expr,$typ:ty) => {
        $a as $typ + $b as $typ
    };
}

fn main() {
		// 这里 add! 宏可以使用多种数据类型
    println!("{}", add_as!(0, 2, u8));
		println!("{}", add_as!(0, 2, u16));
}
```

Rust 宏也支持接受非固定数量的参数。操作符与正则表达式非常相似，`*`用于零个或多个标记类型，`+`用于零个或一个参数。

```rust
macro_rules! add{
    // 匹配单个参数
    ($a:expr)=>{
       $a
    };
   // 匹配2个参数
    ($a:expr,$b:expr)=>{
       {
           $a+$b
       }
    };
   // 递归调用
    ($a:expr,$($b:tt)*)=>{
        {
            $a+add!($($b)*)
        }
    }
}

fn main() {
    println!("{}", add!(1, 2, 3, 4));
}
```

重复的标记类型包含在`$()`中，后面跟着一个`*`或`+`，表示该标记将重复的次数。`$($b:tt)*`表示`tt`类型的参数`$b`，可以重复0~N次，而`add!($($b)*)`则表示多个`$b`会递归调用`add!`宏，因此也就实现了非固定数量的参数调用。

# Example/示例代码

这里我们展示了动态数组`vec!`宏的简化逻辑，以及展开后的代码。

```solidity
macro_rules! vec {
		// $x:expr，即 expr 类型的变量 $x
		// ($(标记的类型),*)，即标记的类型重复多次
    ( $( $x:expr ),* ) => {
        {
            let mut temp_vec = Vec::new();
						// 这里执行多次 push 命令
            $(
                temp_vec.push($x);
            )*
            temp_vec
        }
    };
}

fn main() {
	let v = vec!([1,2,3]);
}

// 展开后的代码如下
let v = {
    let mut temp_vec = Vec::new();
    temp_vec.push(1);
    temp_vec.push(2);
    temp_vec.push(3);
    temp_vec
}
```