# Content/概念

**生命周期**：Rust中的每一个**引用**都有其生命周期（`lifetime`），也就是引用保持有效的作用域。在大多数时候，我们无需手动的声明生命周期，因为编译器可以自动进行推导，但当多个生命周期存在，如同上节的`longest`函数：`fn longest(x: &str, y: &str) -> &str {……}`，入参有2个不同引用，出参也会根据函数体逻辑指向不同的引用，此时编译器无法进行引用的生命周期分析，就需要我们手动标明不同引用之间的生命周期关系，也就是生命周期标注。

**生命周期标注**并不改变任何引用的生命周期的长短。它只是描述了多个引用生命周期相互的关系，便于编译器进行引用的分析，但不影响其生命周期。它的目的是避免悬垂引用，防止程序引用了本不该引用的数据。

**生命周期标注的语法**：生命周期参数名称必须以撇号`'`开头，其名称通常全是小写，类似于泛型其名称非常短。`'a` 是默认使用的名称。生命周期参数标注位于引用的 `&` 之后，并有一个空格来将引用类型与生命周期标注分隔开。

- 比喻
    
    生命周期即 Rust 中值的生老病死，而生命周期标注就是用于约定多个引用之间共生共死的关系，就像桃园三结义中誓约的那样：不求同年同月同日生，但求同年同月同日死，这三兄弟之间的誓约就如同Rust中的生命周期标注，誓约是为了防止有人背信弃义，而Rust生命周期标注是为了编译器进行分析，防止出现悬垂引用。有了誓约并不代表大家就一定一起赴死，就如同生命周期标注并不改变值的生命周期一样。
    
- 真实用例
    
    solana 中`AccountInfo`结构体的生命周期如下，`'a`是泛型生命周期参数，表明结构体的所有引用字段享有相同的生命周期，这确保了结构体的引用在结构体实例生命周期内都是有效的。
    
    ```rust
    pub struct AccountInfo<'a> {
        pub key: &'a Pubkey,
        pub lamports: Rc<RefCell<&'a mut u64>>,
        pub data: Rc<RefCell<&'a mut [u8]>>,
        pub owner: &'a Pubkey,
        pub rent_epoch: Epoch,
        ……
    }
    ```
    

### Documentation

对于函数的参数和返回值中存在多个引用，需要手动去标记生命周期。

```solidity
fn longest<'a>(x: &'a str, y: &'a str) -> &'a str {
    if x.len() > y.len() {
        x
    } else {
        y
    }
}
```

参数`x`和`y`的生命周期标注都是`'a`，至于 'a 究竟是多久我们并不需要关心，只需要知道 'a 代表的是变量 x 和 y 生命周期相同（重叠）的那部分，即 x 和 y 生命周期中最小的那个范围。而返回值也是通过 'a 进行标注的，说明了返回值的生命周期与变量 x 或 y 中最小的那个一致。我们通过FAQ来看下具体的使用例子。

### FAQ

**Q：longest函数是如何处理具有不同生命周期的引用？**

A：如下的代码展示了`string1`和`string2` 这两个不同生命周期的变量，前者的生命周期位于**外部**的`{}`中，而后者的生命周期位于**内部**的`{}`中，所以`'a`代表的生命周期范围是两者中较小的那个，即内部的 {}，此时返回值`result`的生命周期也是属于内部的 {}，即返回值能够保证在 string1 和 string2 中较短的那个生命周期结束前有效，此时不会发生悬垂引用，编译通过。

```rust
fn main() {
    let string1 = String::from("abcdefghijklmnopqrstuvwxyz");
    {
        let string2 = String::from("123456789");
        let result = longest(string1.as_str(), string2.as_str());
        println!("The longest string is {}", result);
    }
}
```

接下来，让我们尝试另外一个例子，该例子揭示了 result 的引用的生命周期必须是两个参数中较短的那个。

```rust
fn main() {
    let string1 = String::from("abcdefghijklmnopqrstuvwxyz");
    let result;
    {
        let string2 = String::from("123456789");
        result = longest(string1.as_str(), string2.as_str());
    }
    println!("The longest string is {}", result);
}
```

此时 `'a` 代表的生命周期范围依旧是变量 `string1` 和 `string2` 中最小的那个，即内部的`{}`，但返回值 `result`的生命周期范围却是外部的`{}`，而不是内部的{}，也就意味着 result 可能会引用一个无效的值，因此编译失败。

> 注意：通过人为观察result的引用应该为 string1，这样返回值result和string1的作用域是一致的，理论上是应该编译通过的。但是，Rust 的编译器会采用保守的策略，我们通过生命周期标注告诉 Rust，longest 函数返回值的生命周期是传入参数中较小的那个变量的生命周期，因此借用检查器不允许上述代码，因为可能存在无效引用。
> 

# Example/示例代码

接下来我们再巩固下，看下结构体定义中的生命周期标注。

```solidity
// 结构体名称后 + 尖括号来标记生命周期
struct MyEnum<'a> {
        // 属性字段使用枚举中标记的生命周期 'a
        // 意味着 greet 引用的生命周期必须要大于枚举实例，否则会发生无效引用
    greet: &'a str,
}

fn main() {
    let hello = String::from("hello, hackquest");
        // 引用的生命周期大于结构体实例，因此可以正常编译
    let i = MyEnum { greet: &hello };
}
```