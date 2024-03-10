# Content/MintNFT

In this section, we'll begin constructing the ***MintNFT*** struct, which is a crucial foundation for our NFT minting functionality.

```rust
#[derive(Accounts)]
pub struct MintNFT<'info> {}
```

Let's break down and understand the basic components and functions of these two lines of code:

1. `#[derive(Accounts)]`： Recalling the basics of Anchor from previous lessons, we know this derive macro facilitates deserialization of the given structure's data, automatically generating account operations and more.
    
    > A more detailed explanation is that, with this derive macro, manual iteration over accounts and deserialization operations are no longer needed. It also implements security checks necessary to ensure the account meets the requirements for safe program execution.
    > 
2. `pub struct MintNFT<'info> {}`：This defines a public structure named `MintNFT`. `<'info>` is a lifetime parameter, indicating that all references within the struct must be valid within the same lifetime.

And that's just the beginning! In our next episodes, we'll be filling this empty structure with all sorts of cool fields, each representing a key player in our NFT minting saga. Stay tuned as we bring our digital art to life! 🌟🎨🚀

**Syntax** 

macro struct

- hint
    
    ```rust
    #[derive(Accounts)]
    pub struct MintNFT<'info> {}
    ```