# Content/概念

> 前言：我们在上一节介绍了字符串切片（String slice），类型为 `&str`，它是指向动态字符串的一个引用，本节我们介绍另一种字符串切片：字符串字面量，可以把它理解成指向静态字符串(程序二进制文件)的一个引用。
> 

**字符串字面量（String Literals）**：是指在代码中直接写死的、由双引号包围的一系列字符，例如 `"Hello, world!"`。它硬编码到最终的程序二进制中，类型为 `&str`，跟我们上节的动态字符串切片类型一样，因为它也是一种字符串引用，对程序二进制文件中静态分配的字符串数据的引用，也称之为静态字符串切片。

- 比喻
- 真实用例
    
    solana中使用`msg!`宏来打印程序（智能合约）的日志，这里的日志通常为字符串字面量，如下：
    
    ```rust
    use solana_program::msg;
    
    msg!("Hello World Rust program entrypoint");
    ```
    

### Documentation

我们接下来分别看下字符串字面量和动态字符串的语法。

```solidity
// 字符串字面量，编译时已确定
let x: &str = "hello world";

// 动态字符串
let hello: String = String::from("hello world");
// 字符串切片，引用整个字符串
let y: &str = &hello[..];
// 字符串切片，引用部分字符串
let z: &str = &hello[0..3];
```

### FAQ

**Q：字符串字面量 和 动态字符串切片的异同点？**

A：**相同点**：①都是都是对字符串数据的引用，而不是实际的字符串数据本身。
②都是UTF-8编码的字符串。③两者都可以使用一些相似的字符串操作，如切片、查找、比较等。**不同点**：①字符串字面量被硬编码到程序二进制文件中，因此在整个程序运行期间有效。而字符串切片取决于引用它的变量或数据结构的生命周期。②字符串字面量在编译时已知大小，是固定大小的；字符串切片在运行时确定大小，是动态大小的。

# Example/示例代码

字符串字面量跟动态字符串切片在语法上一样，都可以通过索引来获取指定范围的数据。

```solidity
// 字符串字面量
let a: &str = "hello, hackquest.";
println!("{} go go go !", a);
// Rust在编译时就会把变量a硬编码到程序中，所以编译后的第5行代码应该长这个样子。
// println!("hello, hackquest. go go go !");

// 通过索引获取 hello
let b = &a[..5];
println!("{}", b);

// 获取动态字符串切片
let s1: String = String::from("hello,world!");
let s2: &str = &s1[..5];
println!("{}", s2);

// 动态字符串转成字符串字面量
let s3: &str = s1.as_str();

// 字符串字面量转成动态字符串类型
let s4: String = "hello,world".to_string();
let s5: String = String::from("hello,world");
```