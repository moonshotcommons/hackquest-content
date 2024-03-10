# Content/**元数据创建**

还记得前面我们学习了如何导入 `create_metadata_accounts_v2` 函数吗？它是 **Metaplex** 框架中的一个函数，用于在 Solana 区块链上创建和初始化 NFT 的元数据账户。

**与 NFT 原始 mint 账户有什么区别？**

1. **NFT 账户（Mint 账户）：**
    - 每个 NFT 在 Solana 上都有一个唯一的 mint 账户。
    - 这个账户代表了 NFT 本身，记录了它的存在和唯一性。
    - Mint 账户用于标识 NFT，并控制它的所有权和转移。
2. **NFT 元数据账户：**
    - 当你使用 `create_metadata_accounts_v2` 时，它会为特定的 NFT 创建一个新的元数据账户。
    - 这个账户存储了 NFT 的描述性信息，例如艺术家、标题、图像链接（URI）、版税信息等。
    - 元数据账户与 NFT 的 mint 账户相关联，确保了这些描述性信息可以直接与特定的 NFT 对应起来。

NFT 的 mint 账户和元数据账户是分开的，但它们通过 NFT 的唯一标识（mint 账户的公钥）关联了起来。

**实现 `create_metadata_accounts_v2` 调用：**

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

		invoke(
        &create_metadata_accounts_v2(
            ctx.accounts.token_metadata_program.key(),
            ctx.accounts.metadata.key(),
            ctx.accounts.mint.key(),
            ctx.accounts.mint_authority.key(),
            ctx.accounts.payer.key(),
            ctx.accounts.payer.key(),
            title,
            symbol,
            uri,
            Some(creator),
            1,
            true,
            false,
            None,
            None,
        ),
        account_info.as_slice(),
    )?;
}
```

**参数解释：**

- ***ctx.accounts.token_metadata_program.key()***: 指向 Token Metadata 程序的 key。
- ***ctx.accounts.metadata.key()***: 指向存储 NFT 元数据的账户的 key。
- ***ctx.accounts.mint.key()***: 指向 NFT 的 mint 账户的 key。
- ***ctx.accounts.mint_authority.key()***: 指向铸造 NFT 的授权账户的 key。
- ***ctx.accounts.payer.key()***: 指向支付交易费用的账户的 key。
- ***title, symbol, uri***: 分别代表 NFT 的标题、符号和元数据 URI。
- ***Some(creator)***: 创作者信息。
- ***1, true, false, None, None:*** 其他配置选项（seller_fee_basis_points、is_mutable、update_authority_is_signer、collection、uses），包括版税和是否可更新。

我们已经在 Solana 区块链上为 NFT 创建了详细的元数据，为后续的 NFT 交易和展示提供了必要的信息。

**Syntax** 

function

- 提示
    
    ```rust
    invoke(
            &create_my_metadata(
                // 参数...
            ),
            my_account_info.as_slice(),
    )?;
    ```