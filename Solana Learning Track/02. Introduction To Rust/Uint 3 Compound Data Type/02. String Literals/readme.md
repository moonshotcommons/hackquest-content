# Content

> In the previous section, we covered string slices (`&str`), which are references to dynamic strings. In this section, we'll introduce another type of string slice: string literals. String literals can be understood as references to static strings (within the program binary).
> 

**String Literals:** are sequences of characters enclosed in double quotes, such as `"Hello, world!"`. They are hardcoded into the final program binary, have the type `&str`, similar to the dynamic string slices from the previous section. They serve as references to statically allocated string data within the program binary, also known as static string slices.

- Metaphor
- Use Case
    
    In Solana, the `msg!` macro is used to print logs for a program (smart contract). These logs often consist of string literals. For example:
    
    ```rust
    use solana_program::msg;
    
    msg!("Hello World Rust program entrypoint");
    ```
    

### Documentation:

Let's explore the syntax of string literals and dynamic strings separately.

```rust
// String literal, known at compile time
let x: &str = "hello world";

// Dynamic string
let hello: String = String::from("hello world");
// String slice, references the entire string
let y: &str = &hello[..];
// String slice, references a part of the string
let z: &str = &hello[0..3];

```

### FAQ:

**Q: What are the similarities and differences between string literals and dynamic string slices?**

A: **Similarities:** ① Both are references to string data rather than the actual string data itself. ② Both are UTF-8 encoded strings. ③ Both can use similar string operations, such as slicing, searching, comparing, etc. **Differences:** ① String literals are hardcoded into the program binary, making them valid throughout the program's runtime. String slices depend on the lifetime of the variable or data structure referencing them. ② String literals have a known size at compile time and are fixed-size; string slices determine their size at runtime and are dynamically sized.

# Example

String literals have the same syntax as String slicing, and both can obtain data in a specified range through indexing.

```solidity
// string literal
let a: &str = "hello, hackquest.";
println!("{} go go go!", a);
// Rust will hard-code the variable a into the program when compiling, so the 5th line of code after compilation should look like this.
// println!("hello, hackquest. go go go!");

// Get hello by index
let b = &a[..5];
println!("{}", b);

// Get dynamic string slice
let s1: String = String::from("hello,world!");
let s2: &str = &s1[..5];
println!("{}", s2);

//Convert dynamic string to string literal
let s3: &str = s1.as_str();

//Convert string literal to dynamic string type
let s4: String = "hello,world".to_string();
let s5: String = String::from("hello,world");
```