# Content/接收参数信息

在上一节中，我们定义了 ***initialize*** 函数，并传入了 ***Initialize*** 结构体作为参数。这个结构体包含了初始化过程所需的所有关键信息，如授权用户和计数器账户。现在，我们将详细讲解如何在函数中处理这些传入的参数。

### 具体步骤

首先，我们必须获取到具体的 ***Counter*** 账户并能修改它。

- **接收并修改计数器账户的信息**：
    
    我们的目标是读取并更新 ***Counter*** 账户的数据。为了实现这一点，我们首先需要获取对该账户的可变引用。这可以通过使用 `deref_mut()` 方法来完成。
    
    ```rust
    ctx.accounts.counter.deref_mut()
    ```
    
    `ctx.accounts.counter` 提供了对 ***Counter*** 账户的访问。使用 `deref_mut()`  方法，我们获得了一个可变引用，这意味着我们现在可以读取和修改 ***Counter*** 账户的数据。
    
    > 例如，我们可能需要初始化计数器的值，或者设置授权用户。
    > 

**Syntax**

deref_mut()

- 提示
    
    ```rust
    let counter = ctx.accounts.counter.deref_mut()
    ```