# Content/概念

**泛型**（generics）：是一种强大的编程特性，允许编写可重用、通用的代码，而不必针对特定的数据类型进行硬编码。泛型的核心思想是参数化类型，即通过在定义时使用占位符来表示数据类型。例如，之前章节用到的`Vec<T>`、`HashMap<K,V>`、`Option<T>`数据类型，使用`<T>`表示一个泛型参数（也可以用其他字符替代，如K、V），其中`T`可以在实际使用时替换为任何具体的数据类型。这样的灵活性使得代码更加通用、可读性更强。

- 比喻
    
    想象一下USB接口，它是一种通用的连接标准，可以连接各种设备，如打印机、键盘、鼠标等。无论设备的品牌或型号如何，只要符合USB标准，都可以连接到计算机。这就好比泛型，能够适应多种不同类型的设备连接需求。
    
- 真实用例

### Documentation

假如我们有一个函数`largest`可以用来查找 `i32` 类型数组中的最大元素，现在我们需要它支持 `i64` 类型的数组，怎么办？当然新增一个参数为`i64`类型的函数也可以，除了类型不同外，其他的逻辑跟上一个函数都一样，但未免太繁琐。

```solidity
// 查找 i32 类型数组的最大元素
fn largest_for_i32(list: &[i32]) -> i32 {
    let mut largest = list[0];
    
    for &item in list.iter() {
        if item > largest {
            largest = item;
        }
    }

    largest
}

// 查找 i64 类型数组的最大元素，除了函数的参数和返回值类型不同外，其他跟
// 上一个函数完全一样
fn largest_for_i64(list: &[i64]) -> i64 {
    let mut largest = list[0];

    for &item in list.iter() {
        if item > largest {
            largest = item;
        }
    }

    largest
}
```

那有什么好的办法吗？当然，泛型可以帮我们解决这个问题。将具体类型抽象为泛型`T`，只要它里面的元素支持大小比较即可，这样我们就可以把上面的2个函数抽象成1个泛型函数。

```solidity
fn largest<T>(list: &[T]) -> T {
    let mut largest = list[0];

    for &item in list.iter() {
        // 这里只是做示意说明，实际代码需要增加泛型约束
        if item > largest {
            largest = item;
        }
    }

    largest
}
```

### FAQ

# Example/示例代码

我们在下面的代码中演示下如何在结构体、枚举、方法中使用泛型。

```solidity
// 1.结构体中使用泛型，所有成员的类型都为 T
struct Point1<T> {
    x: T,
    y: T,
}

// 2.结构体中使用泛型，成员可以拥有不同类型
struct Point2<T,U> {
    x: T,
    y: U,
}

// 3.枚举中使用泛型，Option枚举返回一个任意类型的值 Some(T)，或者没有值 None
enum Option<T> {
    Some(T),
    None,
}

// 4.方法中使用泛型，我们为结构体 Point1<T> 实现了方法 get_x，用于返回 x 成员的值
impl<T> Point1<T> {
    fn get_x(&self) -> &T {
        &self.x
    }
}

fn main() {
    // 1.结构体中使用泛型
    let int_point = Point1 { x: 5, y: 10 };
    let float_point = Point1 { x: 1.0, y: 4.0 };

    // 2.结构体中使用泛型
    let p = Point2{x: 1, y :1.1};

    // 3.枚举中使用泛型
    let option1 = Option::Some(1_i32);
    let option2 = Option::Some(1.00_f64);

    // 4.方法中使用泛型
    let x = int_point.get_x();
}
```