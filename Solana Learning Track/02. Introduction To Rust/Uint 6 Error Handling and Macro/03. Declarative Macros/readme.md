# Content

**Learning Objectives:** Understand the implementation logic and applications of declarative macros.

After our preliminary understanding of macros in Rust, in this section, we will continue to explore declarative macros. Let's begin with a quick review of the concept:

**Declarative Macros** (macro_rules!) employ a mechanism similar to `match` (refer to Section 4.2 on pattern matching) and allow developers to create ***pattern matching and replacement rules using macro rules (`macro_rules!`), replacing code based on matched patterns***. Declarative macros are text-based, involving simple text replacement without manipulating the abstract syntax tree (AST).

> The syntax tree is an abstract representation of code, forming a tree-like structure that represents the syntax of the code. In macros, the syntax tree is an abstract structure composed of individual code units, representing the syntax and structure of the code. Macros can generate, modify, or reassemble code by manipulating the syntax tree.
> 
- **Metaphor**
- **Use Case**
    
    The `entrypoint!` macro is a special macro in Solana programs. It is used to declare the program entry point and set up global handlers.
    
    ```rust
    // Declarative macro: Used to declare the Solana program entry point function
    entrypoint!(process_instruction);
    
    // Logic for handling instructions
    pub fn process_instruction(
        program_id: &Pubkey,
        accounts: &[AccountInfo],
        _instruction_data: &[u8],
    ) -> ProgramResult {
            Ok(())
    }
    ```
    

### Documentation

Here is a simple definition of a declarative macro (using the `macro_rules!` keyword) that implements two pattern matching mechanisms based on the number of parameters.

*Note: The Rust compiler, when expanding this macro, does not calculate the sum of two numbers. Instead, it expands to two numbers being added together. The code is as follows:*

```rust
// Macro definition
macro_rules! add {
		// Match 2 parameters, e.g., add!(1,2), add!(2,3)
    ($a:expr,$b:expr) => {
        // Expanded code of the macro
        {
            // Expression addition
            $a + $b
        }
    };

		// Match 1 parameter, e.g., add!(1), add!(2)
    ($a:expr) => {{
        $a
    }};
}

fn main() {
		let x = 0;
    // Using the macro
    add!(1, 2);
    add!(x);
}

// Expanded code of the macro
fn main() {
	{
		1 + 2
	}
}
```

### FAQs:

**Q1: What is the concept of Tokens in Rust macros?**

A: Tokens are the smallest units of Rust code, representing an element in the source code that stands for a part of the syntax. In Rust, Tokens can be keywords, identifiers, operators, symbols, etc. In macros, we need to manipulate and understand these Tokens to generate or transform code.

```rust
macro_rules! add {
    ($a:expr,$b:expr) => {{
        $a + $b
    }};
}
```

In the above code, parameters starting with `$` and followed by `:` denote the type of the parameter. The type of parameter is commonly referred to as `Token`. Common Token types in Rust are:

- Expression (`expr`): Represents an expression in Rust code, e.g., `x + y`, `if condition { true } else { false }`, etc. Numbers are also a type of expression.
- Statement (`stmt`): Represents a statement in Rust code, e.g., `let x = 1;`, `println!("Hello, world!");`, etc.
- Type (`ty`): Represents a type in Rust code, e.g., `i32`, `bool`, `String`, etc.
- Identifier (`ident`): Represents an identifier in Rust code, e.g., variable names, function names, struct names, etc.
- General Token (`tt`): Represents any Token in Rust code and can be used to match and generate Tokens of any type.

**Q2: How do declarative macros achieve more flexibility than functions, such as dealing with uncertain parameter types and a non-fixed number of parameters?**

A: Building on Q1, we can use parameters with the type `ty` as data types, such as `u8`, `u16`, etc. We can modify the above code to make the macro convert the numbers to a specific type before adding them.

```rust
macro_rules! add_as {
    // ty denotes the parameter type
    ($a:expr,$b:expr,$typ:ty) => {
        $a as $typ + $b as $typ
    };
}

fn main() {
		// The add! macro can now use multiple data types
    println!("{}", add_as!(0, 2, u8));
		println!("{}", add_as!(0, 2, u16));
}
```

Rust macros also support accepting a non-fixed number of parameters. The syntax is similar to regular expressions: `*` for zero or more token types and `+` for zero or one parameter.

```rust
macro_rules! add{
    // Match a single parameter
    ($a:expr)=>{
       $a
    };
   // Match 2 parameters
    ($a:expr,$b:expr)=>{
       {
           $a+$b
       }
    };
   // Recursive call
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

The repeated token type is enclosed in `$()` and is followed by a `*` or `+` indicating the number of times the token will be

repeated. `$($b:tt)*` denotes parameters of type `tt` that can be repeated 0 to N times. The `add!($($b)*)` statement recursively calls the `add!` macro, achieving the capability of handling a non-fixed number of parameters.

# Example

Here we show the simplified logic of the Vector `vec!` macro, as well as the expanded code.

```solidity
macro_rules! vec {
		 // $x:expr, that is, a variable of expr type $x
		 // ($(type of mark),*), that is, the type of mark is repeated multiple times
     ( $( $x:expr ),* ) => {
         {
             let mut temp_vec = Vec::new();
						 //Execute multiple push commands here
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

//The expanded code is as follows
let v = {
     let mut temp_vec = Vec::new();
     temp_vec.push(1);
     temp_vec.push(2);
     temp_vec.push(3);
     temp_vec
}
```