# Content/概念

学习目标：了解悬垂引用的概念及原理。

### Concept

**悬垂引用**：尝试使用离开作用域的值的引用。我们在前面的章节介绍过**借用**的概念，就是获取**值**的**引用**，但在这个值本身超出其作用域后，就会被 Rust 内存管理器释放掉（drop），此时如果还尝试使用该引用，就会发生悬垂引用，引发错误。

- 比喻
    
    悬垂引用，就像借出钱的人（债主）先挂了，那借钱的人到底还不还钱？如果不还，那估计所有借钱的人都盼着债主早点挂掉，增加了社会不安因素；如果还，那怎么还？这就类似于在Rust 中某个值发生了引用，后来这个值又被释放，所以原来的引用指向了一个不存在的值，即悬垂引用。社会中的问题是通过法律法规来解决的，而Rust中的悬垂引用是通过编译器的借用检查器（borrow checker）来解决的，我们接着往下看。
    
- 真实用例

### Documentation

```solidity
// 这里我们看下悬垂引用的例子。
{
    let r;
    {
        let x = 5;
        r = &x;
    }
    println!("r: {}", r);
}
```

变量`x`的作用域在内部的`{}`中，此时变量`r` 获取到了 x 的引用，但在内部{}之后，变量 x 被 Rust 释放，由于变量 r 的作用域一直到外部的{}，也就是此时 r 依然有效，但是它的值不存在了，因此变量 r 成了悬垂引用，这就是为什么编译器会提示`x does not live long enough, borrowed value does not live long enough`。

### FAQ

**Q1：借用检查器（`borrow checker`）是如何工作的？**

A：Rust 编译器有一个借用检查器，它比较作用域来确保所有的借用都是有效的。对于上面的例子，借用检查器会对变量的作用域范围进行标注，如下：

```rust
{
    let r;                // ---------+-- 'a
                          //          |
    {                     //          |
        let x = 5;        // -+-- 'b  |
        r = &x;           //  |       |
    }                     // -+       |
                          //          |
    println!("r: {}", r); //          |
}
```

我们会发现变量 r 的作用域是 'a 所标识的范围，而变量 x 的作用域是 'b 所标识的范围，此时 'b 的范围小于 'a，即变量 r 引用的作用域大于值的作用域，借用检查器就会发现这个引用可能是无效的。

**Q2：对于上面的例子，如何才能通过借用检查器的检查？**

A：只需要保证值的作用域 'b 大于 引用的作用域 'a 即可。换句话说，只要债主一直活着，Rust的世界里就认为这个借贷是允许的。

```rust
{
    let x = 5;            // ----------+-- 'b
                          //           |
    let r = &x;           // --+-- 'a  |
                          //   |       |
    println!("r: {}", r); //   |       |
                          // --+       |
}                         // ----------+
```

# Example/示例代码

在函数中会有更复杂的引用关系，即它有可能会发生悬垂引用，也有可能不会，此时借用检查器就无法工作。下面是一段伪代码，只是为了说明函数中悬垂引用的场景。

```solidity
// 获取变量 x 和 y 所引用的字符串中最长的那个
fn longest(x: &str, y: &str) -> &str {
    if x.len() > y.len() {
        x
    } else {
        y
    }
}

// result 指向的是 string2 的引用，但该引用的作用域仅局限于在内部{}，所以在println 时 就会发生悬垂引用
fn main1() {
    let string1 = String::from("123456789");
    let result;
    {
        let string2 = String::from("abcdefghijklmnopqrstuvwxyz");
        result = longest(string1.as_str(), string2.as_str());
    }
    println!("The longest string is {}", result);
}

// 这里交换了string1 和 string2 的值，此时result1 指向了 string1 的引用，由于string1的值的作用域大于引用的作用域，
// 理论上这段代码是可以编译成功的，但实际上依旧会编译失败。
fn main2() {
    let string1 = String::from("abcdefghijklmnopqrstuvwxyz");
    let result;
    {
        let string2 = String::from("123456789");
        result = longest(string1.as_str(), string2.as_str());
    }
    println!("The longest string is {}", result);
}

// 总结：Rust 的编译器并不像人那么智能，相反，它比人更加保守，所以针对如上的代码，必须要有明确的机制来标识作用域，
// 否则，Rust 就会编译不通过。
```