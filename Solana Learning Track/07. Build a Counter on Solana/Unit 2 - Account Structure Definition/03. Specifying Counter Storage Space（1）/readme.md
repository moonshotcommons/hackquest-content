# Content/**Defining the impl Block for Counter**

In the previous lesson, we defined the ***Counter*** struct, which is used to store information related to the counter. To make this struct operate more effectively in Solana accounts, we need to explicitly specify the size of the storage space it occupies.

To do this, we can use Rust's `impl` block to add a specific attribute to the ***Counter*** struct.

The `impl` block is a core feature in Rust, allowing us to define attributes or methods associated with a specific struct. This approach not only increases the readability and organization of the code but also provides an effective way to encapsulate data and behavior, which is a key concept in object-oriented programming.

**Syntax**

impl

- hint
    
    ```rust
    impl Struct {
       
    }
    ```