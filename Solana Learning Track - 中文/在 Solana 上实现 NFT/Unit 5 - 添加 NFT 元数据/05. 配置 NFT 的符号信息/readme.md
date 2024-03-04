# Content/**创建符号**

在本节课中，我们将学习配置与 NFT 相关的符号信息，用于表示 NFT 的符号，比如 "**AZUKI**" 或  Bored Ape Yacht Club 的 "**BAYC**"。

这个字符串

**定义 *symbol* 属性：**

***symbol*** 字符串在 NFT 元数据中用作代币的简称标识。类似于加密资产的代币符号、股票市场中的股票简称。

```rust
pub fn mint_nft(
        ctx: Context<MintNFT>,
        creator_key: Pubkey,
        uri: String,
        title: String) -> Result<()> {
        
		// ... 前面的代码 ...
		let creator_arr = vec![
            mpl_token_metadata::state::Creator {
                address: creator_key,
                verified: false,
                share: 100,
            },
            mpl_token_metadata::state::Creator {
                address: ctx.accounts.mint_authority.key(),
                verified: false,
                share: 0,
            },
     ];

		let symbol = std::string::ToString::to_string("nft_symb");
}
```

在这个例子中，我们使用 *nft_symb* 作为 NFT 的符号，这个符号就可以代表我们的 NFT 项目。

通过定义 ***symbol*** 属性，我们能够在创建 NFT 时为其分配一个明确的、易于识别的标识符，这对于 NFT 的分类和辨识非常有帮助。有了账户信息、创作者信息和 NFT 符号，下节课我们就将学习如何创建元数据账户。

**Syntax** 

string

- 提示
    
    ```rust
    let symbol = std::string::ToString::to_string("my_symbol");
    ```