# Content/概念

**结构体：**是一种自定义数据类型，用于组织和存储不同类型的数据成员。它允许你创建一个包含多个字段的数据结构，每个字段都有自己的类型和名称，使得代码更具可读性和可维护性。通过`struct`关键字定义。

*延伸阅读：结构体在许多编程语言中都存在，尽管具体的实现和语法可能有所不同，比如C语言是结构体的发源地之一；C++继承了C语言的结构体并引入了类，使得结构体的功能更加强大；Go语言中也有结构体的概念，用于定义一组相关字段的数据结构，并且可以有相关的方法，但没有经典的面向对象继承。Java中虽然没有结构体的概念，但它的Class类特性也跟结构体类似，这正是Java面向对象编程的核心特性……*

- 比喻
    
    假如我们想表示一辆汽车的信息，可以使用 Rust 中的结构体，在结构体中定义汽车的属性（比如品牌、型号、颜色、生产年份等），因此这个汽车结构体可以帮我们组织构建汽车的相关信息。
    
- 真实用例
    
    solana 中账户`AccountInfo`是 Solana 智能合约中一个重要的数据结构，用于在合约中访问和操作账户信息。
    
    ```rust
    pub struct AccountInfo {
        /// 账户公钥，用于唯一标识账户
        pub key: &Pubkey,
        /// 账户的 lamports数量，是引用计数智能指针，允许多个地方共享对变量的可变引用
        pub lamports: Rc<RefCell<&mut u64>>,
        /// 账户所持有的数据
        pub data: Rc<RefCell<&mut [u8]>>,
        /// 这个账户的所有者，也是个账户
        pub owner: &Pubkey,
        /// 账户下次需要支付租金的epoch
        pub rent_epoch: Epoch,
        /// 交易是否由该账户的公钥签名
        pub is_signer: bool,
        /// 标识该账户是否可写，如果为 true，则允许对账户数据进行修改。
        pub is_writable: bool,
        /// 该账户是否为可执行的程序
        pub executable: bool,
    }
    ```
    

### Documentation

以汽车为例，我们学习下如何定义结构体：`struct` 关键字 + `Car` 结构体名称 + 清晰明确的字段及类型。

```solidity
struct Car {
    // 品牌
    brand: String,
    // 颜色
    color: String,
    // 生产年份
    year: String,
    // 是否新能源
    is_new_energy: bool,
    // 价格
    price: f64
}
```

### FAQ

- Q：什么是元组结构体(Tuple Struct)，适用什么场景？
    
    A：结构体必须要有名称，但是结构体的字段可以没有名称，这种结构体长得很像元组，因此被称为元组结构体。
    
    如果你希望有一个整体名称，但是又不关心里面字段的名称。例如下面的 `Point` 元组结构体，众所周知 3D 点是 `(x, y, z)` 形式的坐标点，因此我们无需再为内部的字段逐一命名为：`x`, `y`, `z`。
    
    ```jsx
    // 只有结构体名称：Color，没有字段名称
    struct Color(i32, i32, i32);
    // 只有结构体名称：Point，没有字段名称
    struct Point(i32, i32, i32);
    
    let black = Color(0, 0, 0);
    let origin = Point(0, 0, 0);
    ```
    

# Example/示例代码

接下来我们学习下结构体创建、访问、更新的相关语法。

```solidity
// 标准的创建方式
fn build_car(color: String, year: String, price: f64) -> Car {
    Car {
        brand: String::from("Tesla"),
        color: color,
        year: year,
        is_new_energy: true,
        price: price,
    }
}

// 简化后的创建方式
fn build_car2(color: String, year: String, price: f64) -> Car {
    Car {
        brand: String::from("Tesla"),
        // 函数参数和结构体字段同名时，可以直接使用缩略的方式进行初始化
        color,
        year,
        is_new_energy: true,
        price,
    }
}

fn main() {
    // 声明 Car 类型变量（要求变量必须是 mut 类型）
    let mut car1 = build_car2(String::from("black"), String::from("2023-01-01"), 123.00);

    // 访问并修改结构体(通过 . 操作符访问)
    car1.color = String::from("white");
    println!("car1 {:?}", car1);

    // 根据已有的结构体实例，创建新的结构体实例
    let mut car2 = Car {
        color: String::from("greey"),
        // 其他字段从car1中取，..car1 必须在结构体的尾部使用
        ..car1
    };

    println!("car2 {:?}", car2);
}
```