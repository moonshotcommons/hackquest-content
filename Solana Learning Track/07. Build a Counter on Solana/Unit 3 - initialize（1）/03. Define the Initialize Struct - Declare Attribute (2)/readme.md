# Content/Attribute Declaration

In the previous lesson, we addressed the question, 'Where will the counter's data be stored?' Next, let's continue to solve the second question: Who has the authority to initialize this counter?

We still need to add an attribute to the ***Initialize*** struct to answer this.

**Authorized User Account - authority**:

- This attribute represents the account that has permission to perform the initialization.

In on-chain programs, this is typically the program deployer or an administrator. To ensure that this account indeed has permission to execute operations, we use the `Signer` type.

```rust
pub authority: Signer<'info>,
```

The `Signer` type is used to indicate that this account is a signer, meaning it has the authority to conduct transactions or operations.

Of course, the authorized user is *mutable*, meaning it can be modified during the execution of the program. This is necessary because when an account signs a transaction or operation, its state (such as balance) may change.

Therefore, we can use `#[account(mut)]`, this attribute macro indicates that the ***authority*** account is mutable.

```rust
pub authority: Signer<'info>,
```

**Syntax**

#[account(…)] ，Signer，Struct

- hint
    
    ```rust
    #[account(mut)]
    pub authority: Signer<'info>,
    ```