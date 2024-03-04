# Content/概念

学习目标：掌握 Rust 的2种错误处理方式：panic 和 Result 

### Concept

Rust中的错误主要分为2类，**不可恢复错误 panic** 和**可恢复错误 Result。**
`Panic` 是一种非正常的程序终止，通常表示发生了无法恢复的错误，例如数组越界、除零等。在 Rust 中，Panic 可以通过 `panic!` 宏来显式触发。当 panic 发生时，程序会打印错误信息，并在栈展开（stack unwinding）过程中清理资源，最终退出程序。

`Result` 是一种更为正常和可控的错误处理方式，例如文件操作、网络请求等可能发生错误的场景。这些操作可以返回 `Result<T, E>` 类型并交由开发者处理，其中 T 是成功时的返回类型，E 是错误时的返回类型。

- 比喻
    
    
- 真实用例
    
    solana中程序的执行结果用`ProgramResult`表示，其中`ProgramError`是一个枚举类型
    
    ```rust
    enum ProgramResult {
        Ok(()),
        Err(ProgramError),
    }
    ```
    

### Documentation

下面的代码我们分别展示了`panic`错误和`Result<T, E>`错误。其中`T`和`E`是泛型类型参数，T 代表成功时返回的数据类型，而 E 代表失败时返回的错误类型。由于 Result 预导入模块（prelude）已经包含了Result枚举及其成员，所以使用中不需要显式指定前缀`Result::`，如`Result::Ok、Result::Err`，可直接使用 OK 或 Err

```solidity
/*
 * Result的定义如下，
 * 
 * enum Result<T, E> {
 *    Ok(T),
 *	  Err(E),
 * }
 */

// 两数相除
fn divide(a: i32, b: i32) -> Result<i32, String> {
    if b == 0 {
        Err(String::from("Cannot divide by zero!"))
    } else {
        Ok(a / b)
    }
}

// 不可恢复错误
fn main1() {
    // 人为制造一个 panic 的场景，程序运行到此处会中断，不再往下执行
    panic!("This is a panic situation!");
}

// 可恢复错误，使用 Result 类型来处理潜在的错误
fn main2() {
	
    // divide(1, 0) 返回值为 Result 类型，这里通过 match 进行模式匹配，分别处理成功和失败这2种情况
    match divide(1, 0) {
        Ok(result) => println!("Result: {}", result),
        Err(err) => println!("Error: {}", err),
    }
}
```

### FAQ

**Q1：如果错误需要交给上层调用者来处理，错误如何传播？**

A：如果`method_a` 调用 `method_b`时，除了method_b 中处理错误外，还可以选择让调用者 method_a 知道这个错误并决定该如何处理，这称为 **传播（propagating）**错误，这样能更好地控制代码调用，因为调用者 method_a 可能拥有更多的上下文信息或逻辑来决定应该如何处理错误。请看下面错误传播的代码示意

```rust
use std::io;
use std::io::Read;
use std::fs::File;
// 打开并读取文件内容，这里返回值为Result类型，不管正常还是错误，都可以
// 传播给上层调用者 main 函数
fn read_file_contents(file_path: &str) -> Result<String, io::Error> {
    // 尝试打开文件
    let my_file: Result<File, io::Error> = File::open(file_path);
    
    // 采用模式匹配，如果打开成功，则将文件句柄绑定到 file 变量，
    // 否则采用 Return 显式返回错误信息，交由上层调用者 main 函数处理
    let mut file = match my_file {
        // 等同于 Result::Ok(file)
        Ok(my_file) => my_file,
        Err(e) => return Err(e),
    };

    let mut contents = String::new();

    // 这是一个表达式，模式匹配后直接返回对应的值
    // 如果读取成功，则返回 Ok(contents)，反之，返回 Err(e)，上层调用者 main 
		// 函数处理函数调用的最终结果
    match file.read_to_string(&mut contents) {
        Ok(_) => Ok(contents),
        Err(e) => Err(e),    
    }
}

fn main() {
	// 这里处理函数的调用结果
	match read_file_contents("example.txt") {
		Ok(contents) => println!("File contents: {}", contents),
		// 上层调用者决定只打印错误信息，而不是中断程序执行
		Err(err) => eprintln!("Error reading file: {}", err),
	}
}
```

# Example/示例代码

使用`Result + match` 模式匹配会有大量的样板代码，Rust 提供了一种简化错误传播的语法糖：`?`。它的作用是在函数中将 Result 的 `Ok` 值直接返回，而在遇到 `Err` 时，将其包装在 Err 中并中止函数的执行，将错误传播给调用方。这样可以有效地减少错误处理代码的嵌套，使得代码更加清晰和紧凑。

```solidity
use std::fs::File;
use std::io::{self, Read};

fn read_file_contents(file_path: &str) -> Result<String, io::Error> {
    // 尝试打开文件，
	  // ? 表示如果成功则将文件句柄绑定给变量 my_file，否则直接返回 Err(e)
    let mut my_file = File::open(file_path)?;

    // 尝试读取文件内容
    let mut contents = String::new();
	
	  // ? 表示如果成功则把文件内容绑定给 变量contents，程序继续执行，否则直接返回 Err(e)
    my_file.read_to_string(&mut contents)?;

	  // 返回成功时的文件内容
    Ok(contents)
}

fn main() {
    // 调用带有?的函数
    match read_file_contents("example.txt") {
        Ok(contents) => println!("File contents: {}", contents),
        Err(err) => eprintln!("Error reading file: {}", err),
    }
}
```