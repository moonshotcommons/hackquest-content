# Content/**定义** `mint_authority`  **属性**

在这一节课中，我们将开始完善 **MintNFT** 结构体的属性。

首先，我们第一个定义的是 ***mint_authority*** 属性，它负责交易的授权和签名，简而言之，就是定义了谁有权限发起 NFT 铸造操作。

**添加 *mint_authority* 字段：**

```rust
#[derive(Accounts)]
pub struct MintNFT<'info> {
    #[account(mut)]
    pub mint_authority: Signer<'info>,
}
```

- `Signer<'info>`：***mint_authority*** 是 `Signer` 类型，表示进行 NFT 铸造操作的账户，支持进行交易、签名的操作。
- `#[account(mut)]`：这个属性宏表示 ***mint_authority*** 是一个可变的账户引用。因为在执行铸造过程中，这个账户的状态可能会发生变化（如余额），所以我们需要把这个属性标记为可变的。

**Syntax** 

macro struct

- 提示
    
    ```rust
    #[derive(Accounts)]
    pub struct MintNFT<'info> {
    		#[account(mut)]
        pub authority: Signer<'info>,
    }
    ```