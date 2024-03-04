# Content/**记录尝试次数**

经过上一节课的学习，我们已经学习了如何使用 ***rand*** 库生成随机数。在这一节，我们将进一步完善我们的 ***Bulls and Cows*** 游戏，通过添加一个整数变量用于跟踪记录玩家猜测的次数。

### **添加尝试次数的记录**

游戏中，跟踪玩家尝试的次数是一个重要的功能，它不仅可以用来显示玩家的当前进度，还可以用来决定游戏何时结束。

```rust
let mut attempts = 0;
```

- 声明**可变变量 *attempts*** ：在 Rust 中，**可变变量**允许我们在其生命周期内更改其值。对于记录玩家尝试次数这个属性来说，需要定义为**可变变量**，因为每次玩家猜测时，我们都需要更新这个计数。
- **初始化变量**：初始化 ***attempts*** 变量为0，表示在游戏开始时，玩家尚未进行任何尝试。

简而言之，这行代码声明了一个名为 ***attempts*** 的可变变量，并初始化为0。

**Syntax**

**Mutability**

- 提示
    
    ```rust
    let mut number = 0;
    ```
    

# Quiz/小测

# QuizA

声明一个可变变量 ***attempts*** 并初始化为 *0*，用来记录玩家尝试次数。

```rust
use rand::Rng;

fn main() {
    println!("Welcome to Bulls and Cows");
    let secret_number = rand::thread_rng().gen_range(1..11);
    @@@
    let mut attempts = 0;
    ###

    //regex starts here
    ^let\s+mut\s+attempts\s*=\s*0\s*;\s*$
    //regex ends here
}
```