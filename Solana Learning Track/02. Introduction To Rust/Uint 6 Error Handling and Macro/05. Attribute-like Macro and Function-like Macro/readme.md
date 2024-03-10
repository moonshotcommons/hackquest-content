# Content

Building upon the foundation of the previous sections, let's delve into ***attribute-like macros*** and ***function-like macros***.

Note: Some refer to them as ***class attribute macros*** and ***class*** F**unction-like *macros***, but the term "class" here doesn't relate to the object-oriented programming concept of `class`. Instead, it implies a similarity. Therefore, translating it as "attribute-like" and "function-like" is more apt.

**Attribute-like macros** : Define new external attributes that can be added to annotated items. These macros are invoked using `#[attr]` or `#[attr(...)]` syntax, where `...` represents specific attributes for the annotation (optional).

A simple framework for defining an attribute-like macro is as follows:

```rust
use proc_macro::TokenStream;

// Specify the macro type here
#[proc_macro_attribute]
pub fn custom_attribute(input: TokenStream, annotated_item: TokenStream) -> TokenStream {
    annotated_item
}
```

It's important to note that, unlike derive macros and function-like macros, attribute-like macros have two input parameters instead of one.

- The first parameter is the delimited token stream following the attribute name (i.e., `(…)` in `#[attr(…)]`). If there are no additional attributes (e.g., `#[attr]`), the value of this parameter is empty.
- The second parameter is the token stream of the annotated code item itself, which can be a field, struct, function, etc. (see a real example).
- **Metaphor**
    
    
- **Use Case**
    
    Below is an example of the `#[account(..)]` attribute-like macro used in the Solana Anchor framework. It initializes a PDA account based on the configured attributes. Attributes such as `init`, `seeds`, `payer`, etc., serve as the first TokenStream parameter in the macro definition. The second TokenStream parameter includes the code item marked by the macro, such as `pub pda_counter: Account<'info, Counter>`. The `Counter` struct is marked with `#[account]` for automatic deserialization by the Anchor framework.
    
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
    

### **Documentation**

The following code demonstrates some common attribute-like macros: `#[cfg(…)]` for conditional compilation, `#[test]` for marking test functions, and `#[allow(...)]` and `#[warn(...)]` for controlling the compiler's warning level.

```rust
// Used for selectively including or excluding code based on conditions
#[cfg(feature = "some_feature")]
fn conditional_function() {
    // This function is compiled only when a specific feature is enabled
}

#[test]
fn my_test() {
    // Test function
}

#[allow(unused_variables)]
fn unused_variable() {
    // Allowing unused variables
}
```

### **FAQ**

**Q: What is a function-like macro?**

A: Function-like macros, like declarative macros, are defined using the `macro_rules!` keyword and are invoked using the `custom_fn_macro!(…)`. However, unlike declarative macros that use pattern matching, function-like macros resemble regular function calls. They can use various Rust syntax features, including conditional statements, loops, pattern matching, making them more flexible and powerful.

The framework for defining a function-like macro is simple, as shown below:

```rust
use proc_macro::TokenStream;

// Specify the macro type here
#[proc_macro]
pub fn custom_fn_macro(input: TokenStream) -> TokenStream {
    input
}
```

As you can see, this is essentially a mapping from one `TokenStream` to another, where `input` is the token stream within the invocation delimiters. For example, for the invocation `foo!(bar)`, the input token stream would be `bar`. The returned token stream will replace the macro invocation.

On the right, we showcase common function-like macros in Rust, as well as the `declare_id!` macro used in the Solana Anchor framework.

# Example

Common function-like macros are shown here.

```solidity
// vec! Macro for creating Vec.
let my_vector = vec![1, 2, 3];

// println! and format! macros for formatting strings.
let name = "World";
println!("Hello, {}!", name);

let formatted_string = format!("Hello, {}!", name);

// assert! and assert_eq! macros for writing assertions.
assert!(true);
assert_eq!(2 + 2, 4);

// panic! Macro used to cause Panic exceptions in the program.
panic!("Something went wrong!");

// env! Macro for obtaining environment variables at compile time.
let current_user = env!("USER");
println!("Current user: {}", current_user);

// declare_id! is a macro used in the anchor framework to declare program IDs
declare_id!("3Vg9yrVTKRjKL9QaBWsZq4w7UsePHAttuZDbrZK3G5pf");
```