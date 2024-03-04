# Content/概念

> 我们在前面章节学习过 Rust 的结构体（struct）、枚举（enum）等数据类型以及方法，并且知道通过方法可以定义类型的行为，本节我们会引入一个新的概念：Trait 特性
> 

**Trait特征：**一个类型的行为由其可供调用的方法构成，如果可以对不同类型调用相同的方法的话，这些类型就可以共享相同的行为了。`Trait`特征是一种将方法签名组合起来的机制，目的是构建一个实现某些目的所必需的行为的集合。总的来说，它是定义类型的共享行为并实现代码的抽象。

- 比喻
    
    我们以大雁和燕子作比喻，它们有各自的行为，比如大雁栖息在湖边，燕子在屋檐下筑巢，这类似与 Rust 中的**方法**。同时，它们都属于候鸟，具有**南迁**行为，我们就可以把这部分共通的行为抽象为 **`Trait`**，并赋予各自的实现，比如大雁以V字形队伍南迁，而燕子则低空快速飞行，飞飞停停。因此，Trait 是对类型方法的抽象，便于我们更好的管理Rust 对象。
    
- 真实用例
    
    solana 中有个名为`Account`的Trait，其中的`get`方法提供了构建AccountInfo的元信息。
    
    ```rust
    // solana_program::account_info::Account
    
    pub trait Account {
        // Required method
    		// 返回值：lamports, data, owner, executable, rent_epoch
        fn get(&mut self) -> (&mut u64, &mut [u8], &Pubkey, bool, Epoch);
    }
    ```
    

### Documentation

这里演示了`Trait`特征如何定义，并在结构体上实现的相关逻辑。

```solidity
// trait 关键字 + MigrateBird 特征名
trait MigrateBird {
    // 定义该特征的方法，参数必须包含&self，因为它是该类型上的行为
    fn migrate(&self) -> String;
}

// 定义大雁结构体
struct WildGoose {
     color : String,
}

// 为 wild_goose 类型实现 migrate_bird 特征
impl MigrateBird for WildGoose {
     fn migrate(&self) -> String {
         "Geese fly in a V-shaped formation".to_string()
     }
}
```

> 注意：如果`Trait`特征方法没有默认实现，则方法定义以分号`;`结尾，即只有方法签名，没有`{}`方法体，因为具体的实现交由各类型负责。
> 

### FAQ

Q：什么是`Trait`特征的默认实现？

A：Trait 是共享的行为，所以我们可以给它赋予默认行为，而类型在必要的时候进行覆盖，否则就使用默认的行为。下面的代码展示了如何定义默认行为。

```rust
// 定义特征，并赋予默认实现 default_migrate
trait MigrateBird {
    fn default_migrate(&self) {
        println!("i am flying to the warm south");
    }
}

struct Swallow {
    color : String,
}

// 这里直接使用默认的实现
impl MigrateBird for Swallow {}

fn main() {
    let small_swallow = Swallow {
        color : String::from("black")
    };
    small_swallow.default_migrate();
}
```

# Example/示例代码

这里我们定义了`WildGoose` 和`Swallow`结构体，它们有自己的方法。同时，也有**南迁**的共同方法，即`Trait`特征：`migrate`。

```solidity
// 大雁结构体
struct WildGoose {
    color: String,
}

// 大雁自身的方法
impl WildGoose {
    // 创建自身实例
    fn new() -> Self {
        WildGoose {
            color: "gray".to_string(),
        }
    }
		// 湖边栖息
    fn inhabit(&self) {
        println!("wild geese perch by the lake");
    }
}

// 燕子结构体
struct Swallow {
    color: String,
}

// 燕子自身的方法
impl Swallow {
    fn new() -> Self {
        Swallow {
            color: "black".to_string(),
        }
    }
		// 屋檐下筑巢
    fn build_nest(&self) {
        println!("swallows build nests under the eaves")
    }
}

// trait特征
trait MigrateBird {
    // 交由各自类型实现
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
```