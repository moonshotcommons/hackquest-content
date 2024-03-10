# Content/概念

前面我们学习了**泛型**和 **Trait** 特性，那么接下来我们稍微深入一点。
**泛型单态化（*monomorphization*）**：是一种编译优化技术，它通过填充编译时使用的具体类型，将通用代码转换为特定代码。与创建泛型函数的步骤相反，编译器寻找所有泛型代码被调用的位置并使用泛型代码针对具体类型生成代码。

- 比喻
- 真实用例
    
    我们还是以 solana 中的`AccountInfo`为例，它实现了`From`这个 Trait，并且该 Trait 支持泛型：
    
    ```rust
    // From特征实现了类型的转换，并且这里为泛型 T，即可以支持多种类型的转换
    pub trait From<T>: Sized {
        // Required method
        fn from(value: T) -> Self;
    }
    
    // IntoAccountInfo 也是个 Trait，这里相当于为 IntoAccountInfo 类型
    // 的结构去实现 From Trait，最终的到 AccountInfo 类型的数据
    impl<T: IntoAccountInfo> From<T> for AccountInfo {
        fn from(src: T) -> Self {
            src.into_account_info()
        }
    }
    ```
    

### Documentation

针对上节中泛型函数`largest`，参数类型为`&T`，这样`i32`、`i64`或者其他类型都可以调用该函数。

```solidity
// T 可以代表任何一种类型
fn largest<T>(list: &[T]) -> T {
    let mut largest = list[0];
    for &item in list.iter() {
        if item > largest {
            largest = item;
        }
    }

    largest
}

fn main() {
    let arr1: [i32; 3] = [1, 2, 3];
    largest(&arr1);
    let arr2: [i64; 3] = [1, 2, 3];
    largest(&arr2);
}
```

但是在编译阶段，对于每种使用不同类型的泛型函数的情况，编译器又都会生成一个具体的函数，以便获得更好的性能。单态后的代码类似于这样。

```solidity
// 重新实例化为 i32类型的函数
fn largest_for_i32(list: &[i32]) -> i32 {
    let mut largest = list[0];
    for &item in list.iter() {
        if item > largest {
            largest = item;
        }
    }
    largest
}

// 重新实例化为 i64 类型的函数
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

总的来说，我们可以使用泛型来编写不重复的代码，而 Rust 将会为每一个实例编译其特定类型的代码。这意味着在使用泛型时没有运行时开销；当代码运行，它的执行效率就跟好像手写每个具体定义的重复代码一样。这个单态化过程正是 Rust 泛型在运行时极其高效的原因。

### FAQ

**Q：什么是特征约束（Trait bound）？**

A：我们先看下`Trait`是如何作为参数传递的，回到上节候鸟`MigrateBird` 的例子，我们定义了一个参数类型为 `MigrateBird` 的`fly`方法，如下：

```rust
// trait特征
trait MigrateBird {
    fn migrate(&self) -> String;
}

// 为大雁实现 Trait特性的 migrate 方法
impl MigrateBird for WildGoose {
    fn migrate(&self) -> String {
        "Geese fly in a V-shaped formation".to_string()
    }
}

// 为燕子实现 Trait特性的 migrate 方法
impl MigrateBird for Swallow {
    fn migrate(&self) -> String {
        "swallow fly fast, but have to rest frequently".to_string()
    }
}

fn fly(item: impl MigrateBird) {
		println!("i am flying to the warm south");
}
```

当然，对于`fly`方法，我们还可以用`Trait bound`的方式实现，这样，只有是`MigrateBird`类型的参数，才可以调用该函数，换句话说，我们把参数的泛型类型限制为`MigrateBird`类型。

```rust
fn fly<T: MigrateBird>(item: T) {
		println!("i am flying to the warm south");
}
```

# Example/示例代码

在 `largest` 函数体中我们想要使用大于运算符（`>`）比较两个 `T` 类型的值。这个运算符被定义为标准库中 trait `std::cmp::PartialOrd` 的一个默认方法。所以需要在 `T` 的 trait bound 中指定 `PartialOrd`，如下：

```solidity
// 1.实现 PartialOrd 的特征约束
fn largest<T: PartialOrd>(list: &[T]) -> T {
    let mut largest = list[0];
    for &item in list.iter() {
				// 只有实现了 PartialOrd 特征，才可以比较大小
        if item > largest {
            largest = item;
        }
    }

    largest
}

// 对于上面的代码，依旧编译失败，因为 list[0] 操作试图将元素移动给largest变量，
// 而只有实现了 Copy 特性的类型才能做到，而对于非 Copy 类型的值，会导致所有权
// 的转移

// 2.实现 copy 的特征约束
fn largest<T: PartialOrd + Copy>(list: &[T]) -> T {
    let mut largest = list[0];
    for &item in list.iter() {
        if item > largest {
            largest = item;
        }
    }

    largest
}

// 3.通过 where 实现特征约束
fn largest<T>(list: &[T]) -> T
where T: PartialOrd + Copy,
{
    let mut largest = list[0];
    for &item in list.iter() {
        if item > largest {
            largest = item;
        }
    }

    largest
}
```