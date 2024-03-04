# Content/概念

**学习目标**：鉴于宏的使用场景大于开发场景，因此本节目标并不要求掌握宏的完整开发流程，了解过程宏的实现原理即可。上一节我们学习了声明式宏，本节我们继续学习过程宏中的派生宏。

**派生宏**（Derive Macros）：通常用于为`struct`结构体、`enum`枚举、`union`类型实现`Trait`特征（见4.5节 Trait特征）。使用时通过`#[derive(CustomMacro)]`这样的语法，允许用户轻松地为自定义类型提供一些通用的实现。前文提到三种过程宏(派生宏、属性宏、函数宏)，它们的工作方式都是类似的：***使用 Rust 的源代码作为输入参数，基于代码进行一系列操作后，再输出一段全新的代码。***

一个过程宏的简单框架如下：

```jsx
use proc_macro::TokenStream;

// 标记类宏的类型
#[proc_macro_derive(CustomMacro)]
pub fn custom_macro_derive(input: TokenStream) -> TokenStream {
    TokenStream::new()
}
```

`proc_macro_derive` 稍微特殊一些，因为它需要一个额外的标识符，此标识符将成为 derive 宏的实际名称，如CustomMacro、Clone、Copy等。

input 输入标记流是添加了 derive 属性的类型，它将始终是 `enum`、`struct` 或者 `union` 类型，因为只有这些类型才可以使用 derive 派生宏。

需要说明的是，过程宏中的**派生宏**输出的代码并不会替换之前的代码，而是在原来代码基础上追加指定宏的 Trait 实现。

- 比喻
- 真实用例
    
    solana 的 Anchor 框架中， `#[derive(Accounts)]`宏应用于指令所要求的账户列表，实现了给定 struct 结构体数据的反序列化，以及安全校验的功能。
    
    ```rust
    // 派生宏
    #[derive(Accounts)]
    pub struct InitializeAccounts<'info> {
    	// 结构体中的字段
    }
    
    ```
    

### Documentation

下面的代码我们定义了一个`Foo`结构体，通常情况下 struct 有许多 Trait 要实现。这里使用了2种方式，一种是常规的`impl`，另一种是使用宏

```solidity
struct Foo { x: i32, y: i32 }

// 方式一
impl Copy for Foo { ... }
impl Clone for Foo { ... }
impl Ord for Foo { ... }
impl PartialOrd for Foo { ... }
impl Eq for Foo { ... }
impl PartialEq for Foo { ... }
impl Debug for Foo { ... }
impl Hash for Foo { ... }

// 方式二
#[derive(Copy, Clone, Ord, PartialOrd, Eq, PartialEq, Debug, Hash, Default)]
struct Foo { x: i32, y: i32 }
```

这种情况下显然通过`derive`宏更加方便。但以上两种方式并没有孰优孰劣，***主要在于不同的类型是否可以使用同样的默认特征实现，如果可以，那过程宏的方式可以帮我们减少很多代码实现。***

### FAQ

**Q：派生宏的实现原理是什么？**

A：我们以`HelloMacro`这个 Trait 特征为例，这里有`MyStruct`和`YourStruct`这2个结构体实现了 Trait 特征的`hello_macro()`函数，并打印出对应的结构体的名称。

```jsx
// 这是一个通用的 Trait 特征
trait HelloMacro {
	fn hello_macro();
}

// 自定义结构体 MyStruct，并实现如上特征
struct MyStruct;
impl HelloMacro for MyStruct {
	fn hello_macro() {
		println!("Hello, Macro! My name is MyStruct!");
	}
}

// 自定义结构体 YourStruct，并实现如上特征
struct YourStruct;
impl HelloMacro for YourStruct {
	fn hello_macro() {
		println!("Hello, Macro! My name is YourStruct!");
	}
}

fn main() {
	MyStruct::hello_macro();
	YourStruct::hello_macro();
}
```

这个`HelloMacro`特征可以对任意结构体使用，并且在打印日志中自动替换成结构体的名称，因此把它定义为宏是比较合适的。按照过程宏定义的模板，我们实现如下的代码：

```jsx
// 引入宏相关的依赖
extern crate proc_macro;
use proc_macro::TokenStream;
use quote::quote;
use syn;
use syn::DeriveInput;

// HelloMacro 宏的实现逻辑
#[proc_macro_derive(HelloMacro)]
pub fn hello_macro_derive(input: TokenStream) -> TokenStream {
	let ast:DeriveInput = syn::parse(input).unwrap();
	impl_hello_macro(&ast)
}
```

前几行代码引入了 macro 相关的依赖： Rust 的`quote`和`syn`库，其中 syn 库用于解析 Rust 代码的 AST（抽象语法树），而 quote 库用于生成 Rust 代码。

主体函数首先使用`syn::parse`函数解析输入的 `TokenStream`，并将其转换为`DeriveInput`类型的`ast`。然后，它调用 `impl_hello_macro`函数，将 ast 作为参数传递给它，生成实现`HelloMacro`特征的 Rust 代码，并将其转换为`TokenStream`，并返回给调用者。因此，当用户使用`#[derive(HelloMacro)]`标记了他的类型后，Rust 编译器在编译前会调用 `hello_macro_derive` 函数，生成相应的代码，即宏的展开。

在介绍`impl_hello_macro`函数之前，我们再来回顾下上节提到的`Token`概念，Token 是 Rust 代码的最小单元，它是源代码中的一个元素，代表了语法的一部分。在Rust中，Token可以是关键字、标识符、运算符、符号等。在宏中，我们需要操作和理解这些 Token，以便生成或转换代码。

例如，在 Rust 中，`let x = 5;`这行代码可以被分解为以下 Token：

- `let`: 关键字
- `x`: 标识符
- `=`: 赋值运算符
- `5`: 数字字面量
- `;`: 分号

而`TokenStream`则是由一系列 Token 组成的序列，它是在宏展开期间传递和操作的数据类型。它表示一段被解析和处理过的代码。TokenStream可以包含多个Token，它们组成了一个代码片段。在宏中，通常会接收一个 TokenStream 作为输入，对其中的 Token 进行处理，然后生成一个新的 TokenStream 作为输出。这种方式允许在编译时进行代码生成或代码转换。

再来看一下一个结构体由哪些部分组成:

```jsx
// vis，可视范围   关键字    ident，标识符   generic，范型
pub              struct    User            <T>        {
	// fields: 结构体的字段
	// vis   ident   type
	pub       name:   &T,
}
```

- `pub` : 可视范围，在宏中通过`vis`来表示，表示标识符、模块、结构体等的访问权限。
- `struct` : 关键字`keyword`，例如 `fn`、`struct`、`if` 等。
- `User`:  标识符`ident`，例如变量名、函数名等。
- `<T>`：范型`generic`
- `fields`：结构体字段的集合
- `T`：在 pub name: &T 中表示 ident 的`type`类型，代码中的类型标识符，例如 `i32`、`String` 等。

`syn::parse`调用会返回一个`DeriveInput`结构体来代表解析后的 Rust 代码，后续逻辑我们就是在此基础上调整相应的 Rust 代码，这里大家也许更容易理解为什么说宏是一种元编程了：编写 Rust 代码的代码。

```jsx
DeriveInput {
	// --snip--
	vis: Visibility,
	ident: Ident {
		ident: "MyStruct",
		span: #0 bytes(95..103)
	},
	generics: Generics,
	
	// Data是一个枚举，分别是DataStruct，DataEnum，DataUnion，这里以 DataStruct 为例
	data: Data(
		DataStruct {
			struct_token: Struct,
			fields: Fields,
			semi_token: Some(
				Semi
			)
		}
	)
}
```

接下来看下如何构建特征实现的代码，也是过程宏的具体实现逻辑:

```jsx
fn impl_hello_macro(ast: &syn::DeriveInput) -> TokenStream {
    
    let name = &ast.ident;
    let gen = quote! {
				// 实现 HelloMacro 特征
        impl HelloMacro for #name {
            fn hello_macro() {
                println!("Hello, Macro! My name is {}!", stringify!(#name));
            }
        }
    };
    gen.into()
}
```

首先，将结构体的名称赋予给`name`，也就是 name 中会包含一个字段，它的值是字符串`MyStruct`。

其次，使用`quote!`可以定义我们想要返回的 Rust 代码。由于编译器需要的内容和 quote! 直接返回的不一样，因此还需要使用`.into`方法其转换为`TokenStream`。

特征的`hell_macro()`函数只有一个功能，就是使用`println!`打印一行欢迎语句，使用`stringify!`获取`#name`的字面值形式。有了这个宏，我们就可以直接用它来标记结构体

```jsx
#[derive(HelloMacro)]
struct MyStruct;
```

如上就是过程宏定义的细节，完整的代码见右侧Example。

# Example/示例代码

这里展示了`HelloMacro`的核心逻辑，省略了创建`crate`包的内容。

```solidity
// HelloMacro 宏的定义
extern crate proc_macro;
use proc_macro::TokenStream;
use quote::quote;
use syn;
use syn::DeriveInput;

#[proc_macro_derive(HelloMacro)]
pub fn hello_macro_derive(input: TokenStream) -> TokenStream {

    let ast:DeriveInput = syn::parse(input).unwrap();

    impl_hello_macro(&ast)

}

fn impl_hello_macro(ast: &syn::DeriveInput) -> TokenStream {
    
    let name = &ast.ident;
    let gen = quote! {
				// 派生宏所实现的特征
        impl HelloMacro for #name {
            fn hello_macro() {
                println!("Hello, Macro! My name is {}!", stringify!(#name));
            }
        }
    };
    gen.into()
}

// 宏的使用
#[derive(HelloMacro)]
struct MyStruct;

#[derive(HelloMacro)]
struct YourStruct;

fn main() {
    println!("Hello, world!");
    MyStruct::hello_macro();
    YourStruct::hello_macro();
}
```