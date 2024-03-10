# Content

The **character type** in Rust is represented by the `char` type, occupying `4` bytes of space. It can represent any character in the Unicode character set, including ASCII characters, various symbols, text in various languages, and even emojis. You can create a `char` value using single quotes (`'`). For example, `let a: char = '🦀';`.

The **boolean type** has two values: `true` and `false`, occupying `1` byte of memory.

- **Expansion**
    
    Let's expand a bit on the background knowledge of the character type. Everything a computer processes at the lowest level is a number, including all visible and invisible characters. Each character has a corresponding number, and computers only deal with these numbers. People need to define what character a particular number represents (for example, the number `97` representing the character `a`). In the 1960s, the United States established the `ASCII` character encoding standard, which included 128 characters (English uppercase and lowercase letters, numbers, punctuation marks, as well as some non-printable characters like carriage return, newline, tab, etc.). Back then, 128 characters were sufficient. Later, with the widespread use of computers around the world, people from various countries needed to use computers, and it was not feasible to use only English. Consequently, a character encoding system capable of accommodating all languages, called `Unicode`, was introduced. It maps every single letter, Chinese character, Japanese, Korean, etc., in Unicode to a unique number. It can represent over 110,000 characters.
    However, the Unicode character set is just a mapping between characters and numbers; it is an abstract definition. In the actual usage process (such as displaying and printing text), how this number is stored and transmitted involves encoding methods. Common ones include `GBK`, `UTF-8`, `UTF-16`, and others. Among them, GBK adopts a fixed **double-byte** encoding, meaning each character takes up 2 bytes. On the other hand, UTF-8 is a **variable-length encoding** and can use 1 to 4 bytes to represent a character. For ASCII characters, UTF-8 only needs 1 byte, while other characters may require 2, 3, or 4 bytes. Due to its flexibility, UTF-8 is more popular in many scenarios.
    
- **Real-world Example**
    
    In Solana, the `AccountInfo` struct indicates whether an account has the corresponding attribute using the `bool` type. Its account system is divided into **program accounts** and **data accounts**. The former is responsible for executing logic, while the latter is only responsible for storing data (state). This is quite different from Ethereum's smart contracts, which contain both program and state.
    
    ```rust
    // solana_program::account_info::AccountInfo
    
    pub struct AccountInfo {
        // ……
    
        // Whether it is writable, if True, it is a data account responsible for storing data
        pub is_writable: bool,
        // Whether it is executable, if True, it is a program account responsible for executing logic
        pub executable: bool,
    }
    ```
    

### Documentation

```rust
// English character
let c = 'z';
// Mathematical symbol
let z = 'ℤ';
// Chinese character
let g = '国';
// Emoji
let ferris = '🦀';

// Boolean type
let m = true;
```

### FAQ

- **Q: What is the short-circuit principle when performing logical operations on boolean types?**
    
    A: For the `& and` operation `(a & b)`, if the first operand `a` is `false`, the program does not need to evaluate the value of the second operand `b`. This is because, regardless of the value of `b`, the result will be `false`. This is called the short-circuit principle. Similarly, for the `| or` operation `(a | b)`, if `a` is `true`, the program does not need to evaluate the value of the second operand `b`. This is also the short-circuit principle. Therefore, when performing `& and` or `| or` operations, it is generally a good practice to place the expression with less computation at the beginning. This makes it easier to hit the short-circuit principle, avoiding the program from first evaluating complex expressions and affecting efficiency.
    

# Example

Use the `char` type to print characters from various countries and test how many characters there are between `'你'` and `'我'`.

```solidity
use std::thread;
use std::time::Duration;

// This function takes 3 seconds
fn get_calculate_result() -> bool {
		// Simulating complex calculations takes 3 seconds
		thread::sleep(Duration::from_secs(3));
    println!("called this function");
    false
}

fn main() {
    // Print individual characters in various languages
    let thai_char  = 'ก';
    let korean_char = '한';
    let traditional_chinese_char = '繁';
    let indonesian_char = 'ä';
    // Note that str here is a string type, not a character, but the length is 1
    let str = "国";
    println!("thai_char : {}", thai_char );
    println!("Korean: {}", korean_char);
    println!("Traditional Chinese: {}", traditional_chinese_char);
    println!("Indonesian: {}", indonesian_char);
    
    //Test how many characters there are between '你' and '我'
    for i in '你'..='我' {
        print!("{}", i);//你佡佢佣……戏成我，total 4786 char
    }
    
    let f: bool = true;
    // The short-circuit principle is triggered and the get_calculate_result function will not be called for complex calculations.
    // If changed to get_calculate_result() | f, the function will be called first, which will have a performance impact
    if f | get_calculate_result() {
        println!("Success!");
    }    
} 
```
