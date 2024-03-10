# Content/概念

> 前言：我们在前面章节学习过结构体和枚举类型，它们定义了对象的属性（比如 Car 结构体中的品牌、颜色、价格等），但很多时候，光有属性是远远不够的，我们还需要对象的行为（比如行驶、减速等），而方法，就是关于对象行为的描述。
> 

**方法**：是与结构体`structs`或枚举`enums`或特征对象`trait`等特定类型相关联的函数，它们允许你在这些类型上定义行为，并且支持像调用普通函数一样调用该行为。

方法与函数类似：它们使用`fn`关键字和名称声明，可以拥有参数和返回值，以及对应的函数体逻辑。不过方法与函数是不同的，因为方法通过`impl`关键字在结构体或枚举的上下文中定义，并且它们第一个参数总是`&self`，代表调用该方法的结构体实例。

- 比喻
    
    除了刚才提到的Car的例子，我们还可以以超级玛丽（Super Mario）这个游戏的场景进一步阐释，其中的 Mario 会有大小、金币数、闯关数等属性，同样，也需要跳跃、吃蘑菇、获得金币这样的动作，这就类似于我们在 Mario 结构体上，实现相应的方法，只有这样 Mario 才能不断闯关，而我们的程序才能灵活的实现各种功能。
    
- 真实用例
    
    solana 中生成 [`program derived address`](https://docs.solana.com/developing/programming-model/calling-between-programs#program-derived-addresses)PDA账户的方法 `find_program_address`，这是一种由主程序派生出来的没有私钥的账户。返回值元组中第一个元素`Pubkey`为生成的地址，第二个元素为使用的*`bump seed`。*
    
    ```rust
    pub fn find_program_address(
    		// 种子数组，可以包含多个种子
        seeds: &[&[u8]],
    		// 主程序id
        program_id: &Pubkey
    ) -> (Pubkey, u8)
    ```
    

### Documentation

该例子定义了一个 `Rectangle` 结构体，并且在其上定义了一个 `area` 方法，用于计算该矩形的面积。并在main函数中调用该方法。

```solidity
// 结构体定义
struct Rectangle {
    width: u32,
    height: u32,
}

// impl Rectangle {} 表示为 Rectangle 实现方法(impl 是实现 implementation 的缩写) 
impl Rectangle {
    // area方法的第一个参数为 &self，代表结构体实例本身
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

fn main() {
    let rect1 = Rectangle { width: 30, height: 50 };

    println!(
        "The area of the rectangle is {} square pixels.",
        // 这里调用结构体的area方法
        rect1.area()
    );
}
```

### FAQ

**Q1：Rust 中方法跟函数有什么区别？**

A：方法和函数之间的主要区别在于它们与类型的关系以及调用方式。

**方法**与特定的类型（结构体、枚举、trait等）关联；在类型的`impl`块内定义，使用self参数来表示调用该方法的实例；使用点运算符来调用，类似于面向对象语言中的对象方法。

而**函数**则与特定类型无关，是独立存在的；可在任何地方定义，没有self参数，因为它们不与特定实例相关；直接通过函数名调用。

**Q2：枚举中方法如何定义及使用？**

A：枚举中方法定义和使用，跟结构体类似，具体看下下面的代码

```rust
enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}

impl Message {
    fn call(&self) {
        match &self {
            Message::Quit => println!("退出"),
            Message::Move { x, y } => println!("移动到({},{})", x, y),
            Message::Write(text) => println!("写入{}", text),
            Message::ChangeColor(r, g, b) => println!("改变颜色为({}, {}, {})", r, g, b),
        }
    }
}

fn main() {
    let m = Message::Move { x: 1, y: 2 };
		// 调用枚举方法 call
    m.call();

    let n = Message::Write(String::from("hello"));
    n.call();
}
```

# Example/示例代码

下面我们展示了结构体的方法使用中的一些典型场景：方法名跟字段同名、关联函数。

```solidity
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    /* 同名方法：使得代码更加一致和简洁。当你需要获取或者设置结构体的属性时，
     * 可以直接使用属性名称作为方法名，而不需要额外记忆或查阅文档，同时也更符
     * 合直观的阅读和理解方式，降低代码的维护难度。
     */
    pub fn width(&self) -> u32 {
        return self.width;
    }

    // 关联函数，没有 &self 参数
    pub fn new(width: u32, height: u32) -> Self {
        Rectangle { width, height }
    }
}

fn main() {
    // 方法中没有 self 参数，则该方法为关联函数（associated functions）
    // 通常用于初始化实例的场景，调用关联函数 new 来创建结构体对应的实例
    let rect1 = Rectangle::new(30, 50);

    // 方式一、访问 Rectangle 的 width字段
    println!("{}", rect1.width);

    // 方式二、调用Rectangle 的 width 方法，类似于getter()
    println!("{}", rect1.width());
}
```