# Content/**定义 `mint` 属性**

在这一节课中，我们继续完善 ***MintNFT*** 结构体的属性，接下来我们要定义 ***mint*** 字段，用于铸造生成新 NFT 关联的账户。

在 Solana 上，每个 NFT 都有一个与之关联的唯一的 ***mint*** 账户。这个账户的地址被用来标识 NFT，保证每个 NFT 都是独一无二的。

**添加 *mint* 字段：**

```rust
#[derive(Accounts)]
pub struct MintNFT<'info> {
    #[account(mut)]
    pub mint_authority: Signer<'info>,
    #[account(mut)]
    pub mint: UncheckedAccount<'info>,
}
```

- `#[account(mut)]`：这个属性宏表示 ***mint*** 是一个可变的账户引用。在 NFT 铸造过程中，***mint*** 账户的状态可能会发生改变（增加一个新的 NFT），因此我们将其标记为可变的。
- `UncheckedAccount` VS. `Account`
    
    ***mint*** 属性使用 `UncheckedAccount` 作为账户类型而不是 `Account` ，因为：
    
    1. 当你使用 `Account` 类型时，Anchor 框架会自动为你执行一系列检查和验证，例如检查账户的所有权、确保它没有被关闭等；
    2. 而在 NFT 铸造场景，我们使用 `UncheckedAccount` 可以实现自定义的验证和错误处理，带来了更多的控制权和操作的灵活性。

**Syntax** 

macro struct

- 提示
    
    ```rust
    #[derive(Accounts)]
    pub struct MintNFT<'info> {
        #[account(mut)]
        pub myAccount: UncheckedAccount<'info>,
    }
    ```