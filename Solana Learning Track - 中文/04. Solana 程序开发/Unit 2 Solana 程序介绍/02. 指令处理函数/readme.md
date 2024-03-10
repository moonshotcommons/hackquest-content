# Content

学习目标：理解指令处理函数`process_instruction`。

回想一下，Solana 程序帐户仅存储处理指令的逻辑。这意味着程序帐户是“只读”和“无状态”的。程序处理指令所需的“状态”（数据集）存储在数据帐户中（与程序帐户分开）。

### 数据账户的定义

我们的 Solana 程序要实现计数器的累加，那就必须先定义该数据是以何种形式存储在 Solana 链上的，这里我们使用结构体`CounterAccount`，之所以使用`Account`后缀，因为它是一个数据账户（这个概念一开始对从以太坊转过来的开发者来说很困惑，但慢慢的你就会发现这的确是个巧妙的设计）。

```jsx
/// 定义数据账户的结构
#[derive(BorshSerialize, BorshDeserialize, Debug)]
pub struct CounterAccount {
    pub count: u32,
}
```

该结构体中定义了`u32`类型的`count`属性，在我们每次发起交易指令时，它都会+1操作。因为该值的存储和传输都是使用的字节码，要把字节码转为Rust 类型，我们还需要（反）系列化操作，这里需要引入borsh库。

```jsx
use borsh::{BorshDeserialize, BorshSerialize};
```

实际进行（反）系列化操作是通过`BorshSerialize`、`BorshDeserialize`这2个派生宏实现的，该宏的定义如下，它们都是对解析后类型为`TokenStream`的 Rust 代码元数据进行处理，并返回处理后的元数据。

```jsx
#[proc_macro_derive(BorshSerialize, attributes(borsh_skip))]
pub fn borsh_serialize(input: TokenStream) -> TokenStream {
    // 系列化逻辑……
}

#[proc_macro_derive(BorshDeserialize, attributes(borsh_skip, borsh_init))]
pub fn borsh_deserialize(input: TokenStream) -> TokenStream {
    // 反序列化逻辑……
}
```

### 指令处理函数

这个函数的定义我们在前面已经介绍过，这里看下它的实现逻辑。

```jsx
pub fn process_instruction(
		// 程序ID，即程序地址
    program_id: &Pubkey,
		// 该指令涉及到的账户集合
    accounts: &[AccountInfo]) -> ProgramResult {
    
    // 账户迭代器
    let accounts_iter = &mut accounts.iter();

    // 获取调用者账户
    let account = next_account_info(accounts_iter)?;

    // ……
}
```

为了处理指令，指令所需的数据帐户必须通过`accounts`参数显式传递到程序中。这里因为要对数据账户进行累加的操作，所以 accounts 包含了该数据账户，我们通过迭代器获取到该账户`account`。

`account`数据账户是由该程序派生出来的账户，因此当前程序为它的`owner`所有者，并且只有所有者才可以对其进行写操作。所以我们在这里要进行账户权限的校验。

```jsx
// 验证调用者身份
if account.owner != program_id {
    msg!("Counter account does not have the correct program id");
    return Err(ProgramError::IncorrectProgramId);
}
```

# Example/示例代码

完整的指令处理函数代码如下：

```jsx
pub fn process_instruction(
		// 程序ID，即程序地址
    program_id: &Pubkey,
		// 该指令涉及到的账户集合
    accounts: &[AccountInfo],
		// 指令数据
    _instruction_data: &[u8],
) -> ProgramResult {
    msg!("Hello World Rust program entrypoint");

    // 账户迭代器
    let accounts_iter = &mut accounts.iter();

    // 获取调用者账户
    let account = next_account_info(accounts_iter)?;

    // 验证调用者身份
    if account.owner != program_id {
        msg!("Counter account does not have the correct program id");
        return Err(ProgramError::IncorrectProgramId);
    }

    // 读取并写入新值
    let mut counter = CounterAccount::try_from_slice(&account.data.borrow())?;
    counter.count += 1;
    counter.serialize(&mut *account.data.borrow_mut())?;

    Ok(())
}
```