# Content/Module

这是一节交互的内容！在这里你不会学习枯燥的代码，相反你需要回顾一下我们前几章学习的内容，我们会带你到在线 IDE - Ru**st Playground** 当中去和该程序进行交互。

1. 打开 [Rust Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021)
2. 把我们前面的编写好的项目代码粘贴到 `src/lib.rs` 文件：
    
    ```rust
    use std::io;
    use std::cmp::Ordering;
    use rand::Rng;
    
    fn main() {
        println!("Welcome to Bull and Cows");
    
        let secret_number = rand::thread_rng().gen_range(1..11);
    
        let mut attempts = 0;
    
        loop {
            println!("Please input a number:");
    
            let mut guess = String::new();
            io::stdin().read_line(&mut guess)
                .expect("Ops! Something goes wrong");
    
            let guess: u32 = match guess.trim().parse() {
                Ok(num) => num,
                Err(_) => {
                    println!("Please input valid number");
                    continue;
                }
            };
    
            attempts += 1;
    
            if guess < 1 || guess > 10 {
                println!("Please input a number between 1 and 10");
                continue;
            }
    
            match guess.cmp(&secret_number) {
                Ordering::Less => {
                    println!("too small!");
                    if attempts > 5 {
                        println!("tips: you have tried {} times", attempts);
                    }
                }
                Ordering::Greater => {
                    println!("too big!");
                    if attempts > 5 {
                        println!("tips: you have tried {} times", attempts);
                    }
                }
                Ordering::Equal => {
                    println!("Congratulation you're right!");
                    println!("tips: you have tried {} times", attempts);
                    break;
                }
            }
    
            if attempts == 10 {
                println!("You have tried 10 times, game over");
                break;
            }
        }
    }
    ```
    
3. 找到 **Rust Playground** 顶部的工具栏，点击 **RUN 按钮。**
4. 至此，我们的程序就开始运行了。接下来，我们就可以在控制台输入数字，开始我们的猜数游戏了。

恭喜你🎉，完成本课程！

# Content/Placeholder

[rust猜数.mov](./video/rust%E7%8C%9C%E6%95%B0.mov)