# Content/Importing **`mpl_token_metadata`**

Starting from this lesson, we'll learn how to enhance our NFT metadata using the `mpl_token_metadata` library provided by the **Metaplex** protocol. This library offers a series of operations related to NFT metadata, enabling us to define detailed characteristics for our NFTs.

Import two key functions from the **Metaplex** protocol's **`mpl_token_metadata`** library:

1. ***create_master_edition_v3***：This function is used to create a **Master Edition** NFT. It specifies associated metadata accounts, maximum minting amounts, and other parameters, ensuring each NFT is unique.
    
    > **Master Edition** is a unique concept in the Metaplex protocol. It represents the "**original**" of an NFT. Owners of the **Master Edition** can create a limited or unlimited number of copies (known as **Prints**) of the NFT.
    
    In simple terms, the NFTs we created in Unit 3 are just ordinary tokens. The concept of MasterEditions adds more possibilities to the contract standards, establishing an "**original**" NFT. Creators can specify the number of copies to be minted from this main NFT.
    
    This feature is crucial for artists, as it allows them to retain control over the original work while issuing multiple copies.
    > 
2. ***create_metadata_accounts_v2***：This function is used to create and store metadata on the blockchain for each NFT. This includes information about the creator, the title of the work, and more.
    
    ```rust
    use mpl_token_metadata::instruction::{create_master_edition_v3, create_metadata_accounts_v2};
    ```
    

**Syntax** 

use

- hint
    
    ```rust
    use anchor_spl::token;
    ```