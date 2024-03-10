# Content

**Learning Objectives:** In this section, we will start by comprehensively understanding the foundational concepts of macros and familiarize ourselves with several common macros in Rust.

**`Macro`** is a tool for **metaprogramming** that allows developers to write code that generates other code, enhancing code flexibility and reusability. For a more detailed explanation, refer to the FAQs in this lesson. Macros in Rust are divided into two main types:

**`Declarative Macros`** (macro_rules!) allow developers to create pattern matching and replacement rules using macro rules. It replaces code based on matched patterns. Declarative macros are text-based macros, involving simple text replacement without manipulating the abstract syntax tree (AST).

**`Procedural Macros`** enable developers to use Rust code to process input and generate output during the code generation phase. Unlike declarative macros, procedural macros are more powerful and flexible, coming in three main types: derive macros, attribute-like macros, and function-like macros.

Generally, declarative macros are suitable for simple code transformations, relying on text replacement and pattern matching. On the other hand, procedural macros offer more flexibility, allowing the generation and manipulation of the AST during compilation. While more complex, they provide richer functionality, requiring a deeper understanding and usage. The choice between declarative and procedural macros often depends on the complexity of the desired features and the requirements for type safety.

> AST (Abstract Syntax Tree): Rust source code is parsed into lexical units (Tokens) by the compiler, further forming a tree-like structure where each node represents a syntax element such as expressions, statements, function declarations, etc. The tree structure reflects the nesting and hierarchical relationships in the source code.
> 
- **Metaphor**
    
    One can compare Rust macros to "***code templates***" or "***code generators***." Let's understand this concept through a real-world analogy: Imagine running a custom goods factory. Your customers want to order products with specific specifications and styles, but each person's requirements may differ. You can design some generic product templates and, based on customer needs, use these templates to generate custom products. These templates are analogous to macros in Rust. They include common structures and rules, with specific details depending on the customer's customization needs.
    
- **Use Case**
    
    In Solana programs, multiple macros are utilized to streamline the development process, enhance code readability, and allow developers to focus more on implementing business logic without getting overly concerned with low-level details related to Solana accounts and interactions.
    
    ```rust
    // Attribute-like macro: Used to set the Solana program ID
    declare_id!("3Vg9yrVTKRjKL9QaBWsZq4w7UsePHAttuZDbrZK3G5pf");
    
    // Derive macro: Used for (de)serialization
    #[derive(BorshSerialize, BorshDeserialize)]
    struct NoteState {
        title: String,
        body: String,
        id: u64
    }
    ```
    

### Documentation:

Here are some of the most common macros in Rust:

```rust
// Logging macro: println!
println!("hello, micro");

// Dynamic array creation macro: vec!
let _dyn_arr = vec![1, 2, 3];

// Assertion macro: assert!, checks if a condition is satisfied
let x = 1;
let y = 2;
assert!(x + y == 3, "x + y should equal 3");

// String formatting macro: format!
let name = "world";
let _message = format!("Hello, {}!", name);
```

### FAQs:

**Q: What is the difference between macros and functions in Rust?**

A: In Rust, macros and functions are both tools for code reuse, but they have some crucial differences.

Firstly, macros are a **compile-time** tool, while functions are a **runtime** tool. This means macros are expanded and generate code during compilation, while functions are called and execute code during program runtime. Therefore, macros offer more opportunities for optimization and checks during compilation, enhancing program performance and safety.

Secondly, macros can accept any number and type of parameters and generate code of any type during compilation. This flexibility allows macros to be versatile, suitable for various scenarios. For example, macros can be used to generate data structures, define domain-specific languages, or implement code templates.

Additionally, macros can leverage Rust's metaprogramming features. For instance, attributes like `#[derive]` in macro definitions can automatically generate code, reducing the amount of code that needs to be written.

Here's a simple example illustrating how both macros and functions can achieve the same functionality. Suppose we want to write a function to convert a string to uppercase:

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

This function is straightforward, but we can achieve the same functionality using a macro, as shown below:

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

While the macro may appear more complex, its advantages become evident: it can be expanded during compilation, leading to more optimizations and checks, ultimately improving program performance and safety. In the example above, the macro expands directly to the `to_uppercase` method in the generated code, avoiding the need to call the `to_upper_case` function, reducing runtime overhead. Rust compiler transforms the macro into the following code:

```rust
let s = "hello, world!";
let result = s.to_uppercase();
println!("{}", result);
```

In summary, both macros and functions are valuable tools in Rust, and the choice between them depends on specific requirements.

# Example

Here we create a simple declarative macro `double!` to perform simple text replacement.

```solidity
// Macro rules
macro_rules! double {
     ($x:expr) => {
		 // Replace the code and double the expression
         $x*2
     };
}

fn main() {
     let result = double!(5);
     println!("Result: {}", result); // Output: Result: 10
}
```