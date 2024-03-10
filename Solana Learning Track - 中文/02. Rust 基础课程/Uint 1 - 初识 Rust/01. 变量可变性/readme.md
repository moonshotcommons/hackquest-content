# Content/概念

Rust中的变量可以分为**可变变量**和**不可变变量**，通俗来说，就是变量的值是否允许修改，如果在内存中给变量分配完值之后，可以根据需要来修改这个值，那它就是可变变量，反之，不允许这个值再发生变更，那就是不可变变量。前者很容易理解，变量的值在不同场景下会发生变化，它为编程提供了灵活性；后者，也有存在的道理，通过不可变的限制，提供了编程的安全性，特别是在多线程环境下，也减少了一些运行时检查，在一定程度上提升运行性能。

注意：这里提到的是否可变指的是**变量的值**，而非变量的**数据类型**。另外，不可变变量这个特性并不是Rust特有的，在Java中也有类似的概念，比如`String`类型就是不可变变量，当对不可变对象的值进行了类似的修改操作时，本质上是创建了新的对象，而不是修改了这个不可变变量的值。

- 比喻
    
    举个简单的例子，假如有个叫Ferris的同学，从它出生起，身份证号就是不可变的，伴随Ferris的一生（不可变变量在其整个生命周期中都是不可变的），因为不可变，所以在有些场景下非常有用，比如可以在全国公安系统中准确的定位到一个人；但是，像家庭住址、性别（Nothing is impossible）、联系方式等这些，却有可能发生变化，这些变化对Ferris来说也许是非常有必要的。
    
    注：Ferris是Rust社区的吉祥物，就是那个被煮熟的螃蟹🦀🙈
    
- 真实用例
    
    solana 的 hello world 程序（智能合约）中有一个状态变量`GreetingAccount`，记录了程序的调用次数，每次调用时该变量都会 + 1，说明：solana中的**程序（program）**类似于以太坊中的**智能合约**，不过也有不同，前者的程序不包含数据，而后者则包含。后文中我们将统一用**程序（program）**来指代链上的智能合约逻辑。
    
    ```rust
    pub struct GreetingAccount {
        pub counter: u32,
    }
    
    // 这是程序（智能合约）的入口函数
    pub fn process_instruction(
        program_id: &Pubkey, 
        accounts: &[AccountInfo],
        _instruction_data: &[u8]
    ) -> ProgramResult {
    		
        // 用 mut 修饰反序列化获取 GreetingAccount 的实例
        let mut greeting_account = GreetingAccount::try_from_slice(&account.data.borrow())?;
        greeting_account.counter += 1;
    
        Ok(())
    }
    ```
    

### Documentation

我们分别定义2个不同类型的变量，并尝试修改对应的值。

```solidity
fn main() {
    // x 为可变变量，mut即 mutable的意思，该修饰符修饰的变量允许改变
    let mut x = 1;
    println!("x = {}", x); 
    x = 2;
    println!("x = {}", x);

    // y 为不可变变量，如果没有指定mut，则Rust默认为不可变
    let y = 3;
    println!("y = {}", y);
    // 对不可变变量 y 重新赋值，Rust编译器会给出cannot assign twice to immutable variable y的错误提示
    y = 4; 
    println!("y = {}", y);
}
```

### FAQ

- Q1：不可变变量有哪些好处？
    
    A：在Rust中，变量默认是不可变的（`immutable`），对于这类变量，编译器会在编译时对其进行静态检查，以确保在变量的作用域内不会发生对其进行修改的操作，就像刚才我们尝试把 `y` 改成4，编译器就直接告诉你不允许这么做。这种静态检查可以帮助编译器在编译时优化代码，减少一些运行时的检查。
    
    例如，编译器可以在编译时将不可变变量的值嵌入到代码中，而不是在运行时通过内存寻址来访问变量的值。这可以减少对内存的访问和加载操作，从而提高性能。
    
- Q2：如果把变量全部声明为不可变变量 or 可变变量，有什么影响？
    
    A：如果一个变量你不需要它可变，那么你定义为可变变量就会损失一定的性能，因为要做`runtime`检查。而如果一个变量你需要它可变，你却声明为不可变，那么你只能通过不断声明新的同名变量来模拟可变，但实际在内存中是创建了一个新的对象，这个时候就会降低代码性能。
    
    总的来说，我们要根据实际情况来定义变量的可变性。
    

# Example/示例代码

这里我们展示了不可变变量（默认类型）和可变变量，相信大家已经对它已经不再陌生🚀

```solidity

fn main() {
    // 不可变变量，默认
    let ferris_id = 1234567890;
    println!("ferris_id_card = {}", ferris_id);

    // 可变变量
    let mut ferris_address: &str = "阳光沙滩01号";
    println!("ferris lived in, {}!", ferris_address);

    // 重新赋值
    ferris_address = "阳光沙滩02号";
    println!("now, ferris lived in, {}!", ferris_address);
}
```