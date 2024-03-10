# Content/概念

**函数**是个很常见的概念，它是一段可重复使用的代码块，用于执行特定的任务或完成特定的操作。函数接受输入参数（可选），执行一系列操作，并返回一个值（可选）。

> 需要注意的是，Rust 代码中的函数和变量名使用*`snake_case`*规范风格。在 snake_case 中，所有字母都是小写并使用下划线分隔单词。而在Java、JavaScript等语言中约定的是`CamelCase`驼峰式命名，当然如果在Rust中使用驼峰式命名程序也能跑起来，只不过代码比较辣眼睛~👀
> 
- 比喻
    
    编程语言中的函数其实跟数学中的函数（如y=f(x))是一个概念，根据输入值求输出值，就像一元二次、三次、多项式等函数那样，程序中的函数也是多种多样的，我们接着往下看。
    
- 真实用例
    
    提到函数我们不得不介绍 solana 中的入口点函数`process_instruction`，这是solana 中程序的执行入口：
    
    ```rust
    // 标记 process_instruction 函数为程序的入口点
    entrypoint!(process_instruction);
    
    // 函数名采用蛇形命名法
    pub fn process_instruction(
    		// 参数必须显式指定类型
        program_id: &Pubkey,
        accounts: &[AccountInfo],
        instruction_data: &[u8]
    		// 函数返回值为 ProgramResult 枚举
    ) -> ProgramResult {
        msg!("Hello, world!");
    
        Ok(())
    }
    
    // 返回值类型为枚举，成员变量为 Result 类型
    enum ProgramResult {
    		// 可省略Result::前缀，直接使用 OK
        Ok(()),
    		// Err的值仍是一个枚举类型
        Err(ProgramError),
    }
    
    // 错误枚举
    pub enum ProgramError {
        Custom(u32),
        InvalidArgument,
        InvalidInstructionData,
    		……
    }
    ```
    

### Documentation

现在我们来看下函数的各个组成部分。需要注意的是，**函数的参数需要显式的标注类型**，不仅有助于提高代码的可读性，也有助于 Rust 提供更强的类型安全性，帮助编译器在类型不匹配时发现错误，提供有用的错误信息。

```solidity
// fn 为声明函数的关键字
// unsafe_add()是函数名，函数的命名要遵循 snake_case 的规范，同时要见名知意，提高代码的可读性
// i 和 j 是入参，并且需要显式指定参数类型
// --> i32 表明出参也是 i32 类型
fn unsafe_add(i: i32, j: i32) -> i32 {
   // 表达式形式，所以函数会在计算求和后返回该值
   i + j
}
```

我们在前面章节了解到整数相加可能会**溢出**，但这里并没有特殊处理，所以`unsafe_add`更容易提醒开发者，这个相加是不安全的，要注意啦~

### FAQ

**Q1：Rust 为什么要设计没有任何返回值的单元类型() ?**

A：Rust是一门静态类型语言，它在编译时需要确定每个函数的返回类型。
当函数体中没有返回语句或表达式时，编译器无法确定函数的返回类型应该是什么。为了解决这个问题，Rust引入了单元类型`()`作为一种特殊的类型，表示没有返回值的函数。类似于其他语言中的`void`类型，通常用于打印消息、写入文件等一些不需要返回值的操作。

**Q2：什么是发散函数（Diverging Functions）?**

A：指的是永远不会返回的函数，甚至连默认的`单元类型()`返回值都没有，这些函数通常用`!`类型来标注。通常用于处理错误或不可恢复的情况，并通过终止程序的执行来表达这种状态。

# Example/示例代码

我们在这里展示 Rust 特有的一些函数：表达式作为返回值的函数、单元类型`()`作为返回值的函数 以及 永不返回的发散函数。

```rust
// 表达式作为返回值的函数
fn max_plus_one(x: i32, y: i32) -> i32 {
    if x > y {
        // 命中该规则，可通过return直接返回
        return x + 1;
    }

    // 最后一行是表达式，可作为函数返回值
    // 注意，这里不能有分号，否则就是语句
    y + 1
}

// 单元类型()作为返回值的函数
// 该函数没有显式执行返回值类型，Rust默认返回单元类型()
fn print_hello() {
    // 这里是个语句，不是表达式
    println!("hello");
}

// 永不返回的发散函数，用!标识
fn diverging() -> ! {
    // 抛出panic异常，终止程序运行
    panic!("This function will never return!");
}
```