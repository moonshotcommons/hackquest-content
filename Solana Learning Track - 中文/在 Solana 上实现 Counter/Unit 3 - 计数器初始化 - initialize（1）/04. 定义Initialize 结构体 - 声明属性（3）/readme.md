# Content/属性声明

在解决完前面的两个问题后，我们现在只需要最后添加一个属性就基本完成我们这个结构体的定义了。

**系统程序账户 - system_program**

- 用于在Solana上执行一些基本操作。

`system_program` 属性是用于执行Solana上的基本操作，如账户的创建和管理。这个属性是程序与Solana系统级功能交互的桥梁。

```rust
pub system_program: Program<'info, System>,
```

这个属性不需要特殊的配置，因为它仅代表了Solana的系统程序。在程序中，我们经常需要引用 `system_program` 来执行一些基本的区块链操作。

**Syntax**

- 提示
    
    ```rust
    pub system_program: Program<'info, System>,
    ```