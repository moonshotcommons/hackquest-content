# Content/导入 `mpl_token_metadata`

从这节课开始，我们将学习如何完善我们的 NFT 元数据，我们将使用 **Metaplex** 协议提供的元数据库 `mpl_token_metadata` ，它提供了一系列与 NFT 元数据相关的操作，使我们能够为 NFT 定义详细的特性。

导入 **Metaplex** 协议 `mpl_token_metadata` 库中的两个相关函数：

1. ***create_master_edition_v3***：这一函数用于创建 Master Edition NFT，它会指定关联的元数据账户、最大铸造数量等参数，确保每个 NFT 都是独一无二。
    
    > **Master Edition** 是 Metaplex 协议中的一个特殊概念。它代表了一个NFT的“原版”。拥有 **Master Edition** 的用户可以创建该 NFT 的有限或无限数量的复制品（称为Prints）。
    
    简而言之，我们第3章创建的 NFT 仅仅是一个普通的Token，MasterEditions 的概念为合约标准增加了更多的可能性，它的目的是建立了一个“主”NFT，用户可以在这个**主 NFT** 指定需要铸造的副本数量。
    
    这对于艺术家来说是一个重要的功能，因为它允许他们保留原始作品的控制权，同时能够发行多个副本。
    > 
2. ***create_metadata_accounts_v2***：此函数则是用于在区块链上为每个 NFT 实现创建和存储元数据，包括创作者信息、作品标题等。
    
    ```rust
    use mpl_token_metadata::instruction::{create_master_edition_v3, create_metadata_accounts_v2};
    ```
    

**Syntax** 

use

- 提示
    
    ```rust
    use anchor_spl::token;
    ```