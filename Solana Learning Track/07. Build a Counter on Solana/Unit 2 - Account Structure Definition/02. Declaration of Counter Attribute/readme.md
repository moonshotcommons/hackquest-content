# Content/Declaration of Counter Attribute

In the previous lesson, we established the ***Counter*** struct as an account type within the contract. Now, we will define the properties within this struct in detail, ensuring it meets the needs of our counter application.

Let's first outline the information we need to record in the struct for this counter:

- To implement access control, we need to record the *authorized public key*.
- To store the current state of the counter, we need to record the actual *count value*.
- To ensure each account has a unique *address*, we also need a parameter that will be used in conjunction with the public key to generate the account address. The combination of these fields makes the implementation of the counter on Solana more efficient and secure.

In summary, we should now have a data structure like this:

```rust
pub struct Counter {
    // authority: The public key used for access control.
    // count: Records the current state of the counter.
    // bump: A parameter used for address generation.
}
```

**Syntax**

struct

- hint
    
    ```rust
    pub struct Student{
        pub id: u64,
    }
    ```