# Content

学习目标：掌握`solana_program`库 crate 和程序入口点`entrypoint`概念。

回想一下，Solana 网络上存储的所有数据都包含在所谓的帐户中。每个帐户都有自己唯一的地址，用于识别和访问帐户数据。Solana 程序只是一种特定类型的 Solana 帐户，用于存储和执行指令。

### **Solana crate** solana_program

要使用 Rust 编写 Solana 程序，需要用到 Solana 程序的标准库 solana_program。该标准库包含我们将用于开发 Solana 程序的模块和宏。如果您想深入了解solana_program  crate，请查看**[solana_program crate文档](https://docs.rs/solana-program/latest/solana_program/index.html)**。

对于基本程序，我们需要将 solana_program 库中的以下项目纳入作用域：

```jsx
use solana_program::{
    account_info::AccountInfo,
    entrypoint,
    entrypoint::ProgramResult,
    pubkey::Pubkey,
    msg
};
```

- AccountInfo：account_info 模块中的一个结构体，允许我们访问帐户信息。
- entrypoint：声明程序入口点的宏，类似于 Rust 中的 main 函数。
- ProgramResult：entrypoint 模块中的返回值类型。
- Pubkey：pubkey 模块中的一个结构体，允许我们将地址作为公钥访问。
- msg：一个允许我们将消息打印到程序日志的宏，类似于 Rust 中的 `println`宏。

### **Solana 程序入口点**

Solana 程序需要单个入口点来处理程序指令。入口点是使用`entrypoint!`声明的宏。

通过如下方式声明程序的入口点函数：

```jsx
// 声明程序入口点函数
entrypoint!(process_instruction);
```

该指令处理函数我们在前面章节已介绍过，这里不再赘述。

```jsx
fn process_instruction(
		// 当前的程序ID
    program_id: &Pubkey,
		// 该指令涉及到的账户集合
    accounts: &[AccountInfo],
		// 该指令的参数
    instruction_data: &[u8],
) -> ProgramResult;
```