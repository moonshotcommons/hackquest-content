# Content/概念

流程控制是编写程序时至关重要的一部分，它决定了程序的执行流程。Rust 在流程控制方面的语法设计简洁而强大，常见的流程控制语句有 `if表达式`、`for循环`、`while循环`、`loop循环`，这些是构建程序逻辑的重要工具，灵活运用它们可以使程序更加清晰和高效。

- 比喻
- 真实用例
    
    我们看下 solana 中关于电影评论的例子，在用户新增电影评论时，会有一系列的安全校验，校验通过则程序接着执行，否则抛出异常，流程中断。
    
    ```rust
    // 新增电影评论
    pub fn add_movie_review(
        program_id: &Pubkey,
        accounts: &[AccountInfo],
        title: String,
        rating: u8,
        description: String
    ) -> ProgramResult {
    		
    		// 先校验数据合法性，如果评分不在1~5范围，则抛出error，流程中断
        if rating > 5 || rating < 1 {
            msg!("Rating cannot be higher than 5");
            return Err(ReviewError::InvalidRating.into())
        }
    
    		// 流程继续，do something
    
    		// 如果非签名用户，则抛出error，流程中断
        if !initializer.is_signer {
            msg!("Missing required signature");
            return Err(ProgramError::MissingRequiredSignature)
        }
    
        // 流程继续，do something
    
    		// 如果不是PDA 账户，则抛出error，流程中断
        if pda != *pda_account.key {
            msg!("Invalid seeds for PDA");
            return Err(ReviewError::InvalidPDA.into());
        }
        
        // 流程继续，do something
    
    		// 如果占用空间超过1000字节，则抛出error，流程中断
        if total_len > 1000 {
            msg!("Data length is larger than 1000 bytes");
            return Err(ReviewError::InvalidDataLength.into())
        }
    
        // 走完流程，结束
        Ok(())
    }
    ```
    

### Documentation

下面的代码展示了 Rust 中常见的4种流程控制命令，基本覆盖了编程过程中的绝大部分场景。

```solidity
fn main() {
    let condition = true;
    // if else 语法
    if condition {
        // do something
    } else {
        // do something else
    }

    // for循环
    for i in 1..=5 {
        println!("{}", i);
    }

    // while循环
    let mut m = 1;
    while m <= 5  {
        println!("{}!", m);
        m = m + 1;
    }

    // loop 循环
    let mut n = 1;
    loop {
        println!("{}!!", n);
        n = n + 1;
        if n > 5 {
            break;
        }
    }
}
```