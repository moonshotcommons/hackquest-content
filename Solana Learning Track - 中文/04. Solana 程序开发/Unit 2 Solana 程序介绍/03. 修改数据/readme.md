# Content

学习目标：理解指令处理函数`process_instruction`。

本节我们接着学习该指令函数中的读写操作。

### 读取数据账户

通过上一节的账户权限校验，我们可以确定当前的数据账户是正确的，那么接下来，就是读取该账户存储的数据了。

```jsx
let mut counter = CounterAccount::try_from_slice(&account.data.borrow())?;
```

这行代码的目的是从 Solana 数据账户中反序列化出 `CounterAccount` 结构体的实例。

1. `&account.data`：获取账户的数据字段的引用。在 Solana 中，账户的数据字段`data`存储着与账户关联的实际数据，对于程序账户而言，它是程序的二进制内容，对于数据账户而言，它就是存储的数据。
2. `borrow()`：使用该方法获取`data`数据字段的可借用引用。并通过`&account.data.borrow()`方式得到账户数据字段的引用。
3. `CounterAccount::try_from_slice(...)`：调用`try_from_slice`方法，它是`BorshDeserialize`trait 的一个方法，用于从字节序列中反序列化出一个结构体的实例。这里`CounterAccount`实现了`BorshDeserialize`，所以可以使用这个方法。
4. `?`：是一个错误处理操作符，如果`try_from_slice`返回错误，整个表达式将提前返回，将错误传播给调用方。

通过如上方式，我们获取了`CounterAccount`数据账户进行了反序列化，并获取到它的可变借用。

### 修改数据账户

接下来我们就可以对该数据账户进行修改：

```jsx
counter.count += 1;
counter.serialize(&mut *account.data.borrow_mut())?;
```

- 首先对`CounterAccount`结构体中的`count`字段进行递增操作。
- `&mut *account.data.borrow_mut()`：通过`borrow_mut()`方法获取账户数据字段的可变引用，然后使用`*`解引用操作符获取该`data`字段的值，并通过`&mut`将其转换为可变引用。
- `serialize`函数方法，它是`BorshSerialize` trait 的一个方法，用于将结构体序列化为字节数组。
- `?`：是一个错误处理操作符，如果`serialize`方法返回错误，整个表达式将提前返回，将错误传播给调用方。

通过如上的方式，将`CounterAccount`结构体中的修改后的值递增，并将更新后的结构体序列化为字节数组，然后写入 Solana 账户的可变数据字段中。实现了在 Solana 程序中对计数器值进行更新和存储。

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