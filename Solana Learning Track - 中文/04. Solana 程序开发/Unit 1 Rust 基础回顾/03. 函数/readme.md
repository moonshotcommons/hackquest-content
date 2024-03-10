# Content

学习目标：在本节我们会完成一个 Rust 函数的定义。

### 定义函数名称

我们在 Rust 中定义函数时使用fn关键字，后跟函数名和一组括号。

```jsx
fn process_instruction()
```

接下来，我们可以通过引入变量名称及相应的数据类型来向函数添加参数。

### 定义函数参数

Rust 被称为“静态类型”语言，Rust 中的每个值都具有某种“数据类型”。这意味着 Rust 必须在编译时知道所有变量的类型。在可能存在多种类型的情况下，我们必须向变量添加类型注释。

在下面的示例中，我们创建一个名为`process_instruction`的函数，该函数需要以下参数：

- `program_id`为`&Pubkey`类型
- `accounts`为`&[AccountInfo]`类型，即它是 AccountInfo 结构体数组的引用。
- `instructions_data`为`&[u8]`类型，即 u8 类型数组的引用。

请注意 process_instruction 函数中列出的每个参数的类型前面的`&`。在 Rust 中，`&`代表对另一个变量的**引用**。这允许你引用某些值而不获取它的所有权。“引用”保证指向特定类型的有效值。在 Rust 中创建引用的动作称为`borrow`**借用**。

在此示例中，当调用 process_instruction 函数时，用户必须传入所需参数的值。然后， process_instruction 函数引用用户传入的值，并保证每个值都是 process_instruction 函数中指定的正确数据类型。

此外，请注意`&[AccountInfo]`和`&[u8]`周围的方括号`[]`。这意味着accounts 和 instruction_data 参数分别代表 AccountInfo 和 u8 类型的**切片** 。“切片”类似于数组（相同类型的对象的集合），只是长度在编译时未知。换句话说，accounts 和 instruction_data 参数是未知长度的输入。

```jsx
fn process_instruction(
    program_id: &Pubkey,
    accounts: &[AccountInfo],
    instruction_data: &[u8],
)
```

### 定义函数返回值

接下来，我们可以通过在函数后面使用箭头`->`声明返回类型来让函数返回值。

在下面的示例中，process_instruction 函数现在将返回`ProgramResult`类型的值。我们将在下一节中讨论这个问题。

```jsx
fn process_instruction(
    program_id: &Pubkey,
    accounts: &[AccountInfo],
    instruction_data: &[u8],
) -> ProgramResult {
	// do something...
}
```