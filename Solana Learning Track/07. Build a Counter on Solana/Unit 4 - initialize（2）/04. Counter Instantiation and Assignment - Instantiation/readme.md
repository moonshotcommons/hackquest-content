# Content/**Counter Instantiation and Assignment**

In the previous lessons, we successfully obtained a mutable reference to the ***Counter*** account and the ***bump*** value. The next step is to use this information to initialize an instance of the ***Counter*** struct.

1. **Counter Instantiation**

First, let's proceed to create an instance of ***Counter***. Recall that it has three key attributes: ***authority***, ***count***, and ***bump***. Now, let's assign values to these attributes:

```rust
Counter {
    authority: //,
    count: //,
    bump: //,
};
```

- ***authority***: Here, we set this field to the public key of the passed-in ***authority*** account.
    
    ```rust
    ctx.accounts.authority.key
    ```
    
- ***count*** : This is the starting point of the counter, representing the value of the counter at the beginning. As the starting point of the counter, we initialize ***count*** to 0.
- ***bump*** : Finally, we assign the previously extracted ***bump*** value to the ***Counter*** instance.

This way, we have successfully initialized an instance of the ***Counter*** struct, preparing the basic data structure for subsequent operations.

**Syntax**

counter instantiation

- hint
    
    ```rust
    Counter {
                authority: *ctx.accounts.authority.key,
                count: 0,
                bump,
    };
    ```