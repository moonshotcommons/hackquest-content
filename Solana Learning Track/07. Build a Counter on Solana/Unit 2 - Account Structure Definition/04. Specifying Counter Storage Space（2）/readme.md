# Content/**Calculating Counter Storage Space**

In the previous lesson, we defined the `impl` block for ***Counter*** . Next, let's calculate the storage space required for ***Counter*** .

***Counter*** consists of three fields: ***authority***, ***count***, and ***bump***.

First, we need to consider the size of each field and any potential padding space. In Solana, each field is typically stored in *multiples of 8 bytes (64 bits)* for alignment and optimized access.

- ***authority***: Public keys are usually 32 bytes (256 bits).
- ***count***: The `u64` type is 8 bytes.
- ***bump***: The `u8` type is 1 byte.

Therefore, adding up the space occupied by these fields, we should need:

`32 bytes (authority) + 8 bytes (count) + 1 byte (bump) = 41 bytes`

Thus, the ***Counter*** struct needs at least *41 bytes* of storage space in a Solana account. This information is crucial for ensuring the correct account layout and memory allocation. Additionally, an 8-byte account type identifier is needed at the beginning for proper management.

**Syntax**

const

- hint
    
    ```rust
    pub const SIZE: usize = 8 + 32 + 8 + 1;
    ```