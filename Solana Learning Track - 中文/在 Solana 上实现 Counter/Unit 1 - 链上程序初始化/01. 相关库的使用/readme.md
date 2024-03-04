# Content/相关库的使用

现在，让我们开始编写我们的代码吧！首先是导入相关的库。

### **使用 Anchor 框架**

为了充分利用 Anchor 框架的强大功能，我们首先引入 ***anchor_lang*** 。它为我们提供了 Anchor 框架的核心功能和类型定义。

### **使用 DerefMut**

为了让我们可以更自然地修改复杂数据结构，我们需要引入Rust标准库的 ***DerefMut***。这个特性使得操作封装数据就像使用普通变量一样简单，从而简化了代码并提高了可读性。

比如在我们后面需要处理账户数据时，***DerefMut*** 可以使得从账户状态中获取和修改数据更加直接和简洁。

**Syntax**

use

- 提示
    
    ```rust
    use anchor_lang::prelude::*;
    use std::ops::DerefMut;
    ```