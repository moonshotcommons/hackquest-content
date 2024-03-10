# Content/ **`declare_id`**

In this section, we'll learn how to declare a unique ID for our Solana program.

> On the Solana, each program has a unique address, known as the **Program ID**. This ID serves as a unique identifier for the program on the blockchain, making it easy to locate our developed program.
> 

**Using the** `declare_id!` **Macro**

In the Anchor framework, we use the `declare_id!` macro to specify the program's on-chain address. When you first build an Anchor program, the framework will generate a new key pair. The public key of this key pair is your program ID.

```rust
declare_id!("Fg6PaFpoGXkYsidMpWTK6W2BeZ7FEfcYkg476zPFsLnS");
```

Typically, each time you build a Solana program using the Anchor framework, the **Program ID** will be different. However, by using the `declare_id!` macro, you can assign a fixed ID to the program. This way, even if the program is upgraded later, its ID remains unchanged.

**Syntax** 

macro

- hint
    
    ```rust
    declare_id!("Fg6PaFpoGXkYsidMpWTK6W2BeZ7FEfcYkg476zPFsLnS");
    ```