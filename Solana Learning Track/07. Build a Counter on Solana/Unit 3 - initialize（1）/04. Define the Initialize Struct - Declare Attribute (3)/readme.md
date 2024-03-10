# Content/Attribute Declaration

After resolving the previous two questions, we now only need to add one last attribute to essentially complete the definition of our struct.

**System Program Account - system_program**

- Used for executing basic operations on Solana.

The `system_program` attribute is used for performing basic operations on Solana, such as account creation and management. This attribute serves as a bridge between the on-chain programs and Solana's system-level functionalities.

```rust
pub system_program: Program<'info, System>,
```

This attribute does not require special configuration, as it simply represents Solana's system program. In the programs, we often need to refer to `system_program` to perform some basic blockchain operations.

**Syntax**

- hint
    
    ```rust
    pub system_program: Program<'info, System>,
    ```