# Content/Module

This is an *interactive* lesson! Here, instead of learning dry code, you'll revisit the content we've covered in the previous chapters. We'll take you to the online IDE - **Rust Playground** to interact with the program.

1. Open [Rust Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021).
2. Paste the code we wrote earlier into the ***src/lib.rs*** file:
    
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
    
3. Go to the top toolbar of **Rust Playground** and click the **RUN button**.
4. Now, our program has started running. Next, we can input numbers in the **console** to start our guessing game.

🎉Congratulations, you have completed this course!

# Content/Placeholder

[rust猜数.mov](./video/rust猜数.mov)