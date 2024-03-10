# Content/定义账户信息

在本节课中，我们将学习如何配置添加元数据所需的账户数组，这个数组包含了执行 NFT 铸造和元数据创建所需的所有关键账户信息，是实现与 Metaplex 的 Token Metadata 程序交互的基础。

**定义账户数组：**

```rust
pub fn mint_nft(
        ctx: Context<MintNFT>,
        creator_key: Pubkey,
        uri: String,
        title: String) -> Result<()> {
        
		// ... 前面的代码 ...

		let account_array = vec![
        ctx.accounts.metadata.to_account_info(),
        ctx.accounts.mint.to_account_info(),
        ctx.accounts.mint_authority.to_account_info(),
        ctx.accounts.payer.to_account_info(),
        ctx.accounts.token_metadata_program.to_account_info(),
        ctx.accounts.token_program.to_account_info(),
        ctx.accounts.system_program.to_account_info(),
        ctx.accounts.rent.to_account_info(),
    ];
}
```

- ***metadata***: 存储 NFT 的元数据信息，例如名称、描述、图片链接等。
- ***mint***: NFT 的 mint 账户，用于标识 NFT 的唯一性。
- ***mint_authority***: NFT 的铸造授权账户，具有创建 NFT 的权限。
- ***payer***: 支付交易费用的账户。
- ***token_metadata_program***: Metaplex 的 Token Metadata 程序账户，用于创建和更新 NFT 元数据。
- ***token_program***: Solana 的 Token Program 账户，用于执行代币相关操作。
- ***system_program***: Solana 的系统程序账户，用于一些程序基本操作。
- ***rent***: Solana 网络的租金账户，用于支付数据存储的费用。

至此，我们已经配置好了添加 NFT 元数据所需的账户信息，下节课开始，我们会继续学习与 NFT 元数据相关的其他配置信息，创作者、名称、描述等等。

**Syntax** 

array

- 提示
    
    ```rust
    let account_info = vec![
            ctx.accounts.my_account_one.to_account_info(),
            ctx.accounts.my_account_two.to_account_info(),
    ];
    ```