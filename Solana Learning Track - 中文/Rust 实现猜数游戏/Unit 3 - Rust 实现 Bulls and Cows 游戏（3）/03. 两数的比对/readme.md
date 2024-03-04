# Content/内容

在获取并捕获了用户的输入之后，我们就可以完成程序的最后一步了——两数对比

### 数值比较

我们将使用std依赖中的`cmp`和`Ordering`来实现对比功能

> ***cmp()*:** 方法是泛型，可以用于比较**多种类型**的值，比如整数，字符串，浮点数等。
> 

```rust
fn main() {
    let num1 = 42;
    let num2 = 30;

    // 使用cmp方法比较两个整数的大小
    match num1.cmp(&num2) {
        std::cmp::Ordering::Less => println!("{} 小于 {}", num1, num2),
        std::cmp::Ordering::Equal => println!("{} 等于 {}", num1, num2),
        std::cmp::Ordering::Greater => println!("{} 大于 {}", num1, num2),
    }
}
```

首先声明两个变量：`num1` ，`num2` ，通过 ***match()*** 和 ***cmp()*** 方法对比两数，cmp方法将返回一个`std::cmp::Ordering` 的枚举，该枚举类有三个变体：`Less`，`Equal`, `Greater` 我们通过 ***match()*** 表达式来根据比较的结果执行不同的操作。