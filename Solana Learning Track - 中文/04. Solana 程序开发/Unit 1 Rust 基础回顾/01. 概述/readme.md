# Content

前言：通过前面章节的学习，我们对`Solana`的基本概念以及`Rust`的基础语法有了一定的了解，***接下来让我们在 Solana 上实现一个简单的计数器程序，通过这个小 demo 掌握在 Solana 中开发程序的完整流程***。

### 程序介绍

***该程序实现了计数器累加的功能，即每次调用该程序时，内部的计数器会+1***。虽然是个简单的功能，但它覆盖了我们之前学过的如下知识点：

- Rust 基本数据类型、数组、结构体 struct 等
- Rust 函数及错误处理
- Rust 模块系统
- Rust 函数式宏及派生宏
- Solana 账户
- Solana 程序、交易、指令
- Solana 基于浏览器的 IDE：***Playground***
- Solana 程序等编译、部署、测试
- Solana 区块链浏览器
- ……

> 完整的代码在右侧，如果你觉得困惑，没关系，接下来的章节我们会一步步进行介绍。
> 

### 课程安排：

1. Rust 模块系统
2. Rust 函数
3. Rust 结果枚举
4. Solana 程序依赖
5. Solana 程序入口点
6. Solana 指令处理函数
7. Solana 指令函数的返回值
8. Solana 构建和部署
9. Solana 浏览器

# Example

```jsx
use borsh::{BorshDeserialize, BorshSerialize};
use solana_program::{
     account_info::{next_account_info, AccountInfo},
     entrypoint,
     entrypoint::ProgramResult,
     msg,
     program_error::ProgramError,
     pubkey::Pubkey,
};

/// Define the structure of the data account
#[derive(BorshSerialize, BorshDeserialize, Debug)]
pub struct CounterAccount {
     pub count: u32,
}

//Define program entry point function
entrypoint!(process_instruction);

pub fn process_instruction(
//Program ID, that is, program address
     program_id: &Pubkey,
//The set of accounts involved in this command
     accounts: &[AccountInfo],
// command data
     _instruction_data: &[u8],
) -> ProgramResult {
     msg!("Hello World Rust program entrypoint");

     //Account iterator
     let accounts_iter = &mut accounts.iter();

     // Get the caller account
     let account = next_account_info(accounts_iter)?;

     //Verify caller identity
     if account.owner != program_id {
         msg!("Counter account does not have the correct program id");
         return Err(ProgramError::IncorrectProgramId);
     }

     // Read and write new values
     let mut counter = CounterAccount::try_from_slice(&account.data.borrow())?;
     counter.count += 1;
     counter.serialize(&mut *account.data.borrow_mut())?;

     Ok(())
}
```