# Content

**Learning Objectives:** Given that the use cases for macros are broader than development scenarios, the goal of this section does not require mastering the complete macro development process. Understanding the implementation principles of procedural macros is sufficient. In the previous section, we learned about declarative macros, and in this section, we continue with procedural macros, specifically derive macros.

**Derive Macros:** These macros are typically used to implement `Trait` for `struct` structures, `enum` enumerations, or `union` types (see Section 4.5 on Traits). They allow users to easily provide some common implementations for custom types using syntax like `#[derive(CustomMacro)]`. The three types of procedural macros mentioned earlier (derive macros, attribute macros, and function macros) work similarly: **they take Rust source code as input, perform a series of operations based on the code, and then output a completely new piece of code.**

A simple framework for a procedural macro looks like this:

```rust
use proc_macro::TokenStream;

// Define the type of attribute macro
#[proc_macro_derive(CustomMacro)]
pub fn custom_macro_derive(input: TokenStream) -> TokenStream {
    TokenStream::new()
}
```

`proc_macro_derive` is a bit special because it requires an additional identifier, which will become the actual name of the derive macro, such as `CustomMacro`, `Clone`, `Copy`, etc.

The input `input` to the macro is the type with the derive attribute. It will always be a `enum`, `struct`, or `union` type since only these types can use derive macros.

It's important to note that the output code from a procedural macro does not replace the existing code; instead, it appends the implementation of the specified macro trait to the original code.

- **Metaphor**
    
    
- **Use Case**
    
    In the Anchor framework of Solana, the `#[derive(Accounts)]` macro is applied to the list of accounts required by an instruction. It implements deserialization and secure validation for the given struct data.
    
    ```rust
    // Derive macro
    #[derive(Accounts)]
    pub struct InitializeAccounts<'info> {
        // Fields in the struct
    }
    ```
    

### Documentation

The following code defines a `Foo` struct. Typically, a struct has many traits to implement. There are two ways to implement these traits: the regular `impl` way and using macros.

```rust
struct Foo { x: i32, y: i32 }

// Method one
impl Copy for Foo { ... }
impl Clone for Foo { ... }
impl Ord for Foo { ... }
impl PartialOrd for Foo { ... }
impl Eq for Foo { ... }
impl PartialEq for Foo { ... }
impl Debug for Foo { ... }
impl Hash for Foo { ... }

// Method two
#[derive(Copy, Clone, Ord, PartialOrd, Eq, PartialEq, Debug, Hash, Default)]
struct Foo { x: i32, y: i32 }
```

In this case, using the `derive` macro is more convenient. However, there is no clear superiority or inferiority between the two methods. The choice depends on whether different types can use the same default trait implementations. If they can, the procedural macro approach can reduce a significant amount of code.

### FAQ:

**Q: What is the implementation principle of derive macros?**

A: Let's take an example using the `HelloMacro` trait. Here, `MyStruct` and `YourStruct` structs implement the `hello_macro()` function of the trait, printing the name of the respective struct.

```rust
// This is a generic trait
trait HelloMacro {
    fn hello_macro();
}

// Custom struct MyStruct, implementing the above trait
struct MyStruct;
impl HelloMacro for MyStruct {
    fn hello_macro() {
        println!("Hello, Macro! My name is MyStruct!");
    }
}

// Custom struct YourStruct, implementing the above trait
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

The `HelloMacro` trait can be applied to any struct, and it automatically replaces the trait's name in the log with the name of the struct. Therefore, defining it as a macro makes sense: it is a way to write code that writes Rust code.

The `HelloMacro` trait is implemented for any struct, and the macro implementation follows a similar pattern:

```rust
extern crate proc_macro;
use proc_macro::TokenStream;
use quote::quote;
use syn;
use syn::DeriveInput;

// Implementation of the HelloMacro macro
#[proc_macro_derive(HelloMacro)]
pub fn hello_macro_derive(input: TokenStream) -> TokenStream {
    let ast: DeriveInput = syn::parse(input).unwrap();
    impl_hello_macro(&ast)
}

// Implementation of the trait HelloMacro
fn impl_hello_macro(ast: &syn::DeriveInput) -> TokenStream {
    let name = &ast.ident;
    let gen = quote! {
        // Implement the HelloMacro trait
        impl HelloMacro for #name {
            fn hello_macro() {
                println!("Hello, Macro! My name is {}!", stringify!(#name));
            }
        }
    };
    gen.into()
}
```

Firstly, the `syn::parse` function is used to parse the input `TokenStream` into a `DeriveInput` structure, representing the parsed Rust code. Then, the `impl_hello_macro` function is called, passing the `ast` as a parameter. This function generates Rust code to implement the `HelloMacro` trait for the given struct and converts it to a `TokenStream` before returning it.

Before introducing the `impl_hello_macro` function, let's revisit the concept of `Token`. A Token in Rust represents the smallest unit of code, whether it is a keyword, identifier, operator, or symbol. In macros, understanding and manipulating these Tokens is crucial for code generation or transformation.

For example, the line `let x = 5;` in Rust can be broken down into the following Tokens:

- `let`: Keyword
- `x`: Identifier
- `=`: Assignment operator
- `5`: Numeric literal
- `;`: Semicolon

`TokenStream` is a sequence of Tokens, representing a piece of parsed and processed code during macro expansion. It consists of multiple Tokens, forming a code snippet. In macros, you typically receive a `TokenStream` as input, manipulate the Tokens within it, and then generate a new `TokenStream` as output. This allows code generation or transformation at compile time.

Now, let's take a look at the structure of a struct:

```rust
// vis, visibility   keyword   ident, identifier   generic, generics
pub               struct         User               <T>              {
    // fields: Fields of the struct
    // vis   ident   type
    pub     name:   &T,
}
```

- `pub`: Visibility (keyword)
- `struct`: Keyword
- `User`: Identifier
- `<T>`: Generics
- `fields`: Collection of struct fields
- `T`: Type (ident) in `pub name: &T`, representing the type of the

identifier, e.g., `i32`, `String`, etc.

The `syn::parse` call returns a `DeriveInput` struct that represents the parsed Rust code. The subsequent logic adjusts the corresponding Rust code based on this structure. This is where the idea of macros as metaprogramming becomes clearer: writing code that writes Rust code.

Now, let's look at the specific implementation of generating trait implementation code:

```rust
fn impl_hello_macro(ast: &syn::DeriveInput) -> TokenStream {

    let name = &ast.ident;
    let gen = quote! {
        // Implement the HelloMacro trait
        impl HelloMacro for #name {
            fn hello_macro() {
                println!("Hello, Macro! My name is {}!", stringify!(#name));
            }
        }
    };
    gen.into()
}
```

Firstly, the name of the struct is assigned to `name`. Then, using `quote!`, we define the Rust code we want to return. Since the compiler's requirements and what `quote!` directly returns are different, the `.into` method is used to convert it to a `TokenStream`.

The `hello_macro()` function of the trait has one functionality: it prints a welcome statement using `println!` and obtains the literal form of `#name` using `stringify!`. With this macro, we can directly use it to annotate a struct:

```rust
#[derive(HelloMacro)]
struct MyStruct;
```

This is how derive macros work. For the complete code, refer to the Example on the right.

# Example

The core logic of `HelloMacro` is shown here, and the content of creating a `crate` package is omitted.

```solidity
//Definition of HelloMacro macro
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
				// Characteristics implemented by derived macros
         impl HelloMacro for #name {
             fn hello_macro() {
                 println!("Hello, Macro! My name is {}!", stringify!(#name));
             }
         }
     };
     gen.into()
}

//Use of macros
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