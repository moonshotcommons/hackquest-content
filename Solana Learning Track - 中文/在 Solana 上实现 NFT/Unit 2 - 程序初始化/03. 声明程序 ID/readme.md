# Content/**使用 `declare_id`**

这一节，我们将学习如何为我们的 Solana 程序声明一个唯一 ID。

> 在 Solana 区块链上，每个程序都有一个唯一的地址，即程序 ID（Program ID）。这个 ID 用于程序在链上的唯一标识，方便定位我们开发的程序。
> 

**使用** `declare_id!` **宏**

在 Anchor 框架中，我们使用 `declare_id!` 宏来指定程序的链上地址。当您第一次构建一个 Anchor 程序时，框架会生成一个新的密钥对。这个密钥对的公钥就是您的程序 ID。

```rust
declare_id!("Fg6PaFpoGXkYsidMpWTK6W2BeZ7FEfcYkg476zPFsLnS");
```

通常情况下，每次基于 Anchor 框架去构建 Solana 程序时，程序 ID 都会有所不同。但是，我们通过 `declare_id!` 宏可以为程序指定某个固定的 ID，这样后续即使程序升级，它的 ID 仍然不会发生改变。

**Syntax** 

macro

- 提示
    
    ```rust
    declare_id!("Fg6PaFpoGXkYsidMpWTK6W2BeZ7FEfcYkg476zPFsLnS");
    ```