# Content/注解

在上一节完成初始化操作之后，接下来，我们将着手实现链上程序的核心功能——*increment*，即递增计数器的值。

为了实现这一功能，我们需要定义一个专门的结构体来组织和接收执行递增操作所需的信息。类似于初始化过程，递增操作也涉及到多个账户的交互。因此，我们将使用 `#[derive(Accounts)]` 宏来管理这些账户和操作。

还记得我们之前定义初始化结构体的操作吗？模仿它来定义递增结构体。

**Syntax**

#[derive(Accounts)]，<'info> ，Struct

- 提示
    
    ```rust
    #[derive(Accounts)]
    pub struct Increment<'info> {
    }
    ```