# Content/Attribute Declaration

Continuing from the previous lesson, let's look at the second attribute of ***Increment***.

1. **Permission Verification**
    
    To ensure that only authorized users can increment the counter, we need to include a field in the struct that represents user permissions. Typically, this is the user's public key or signer information, used to confirm the user's identity and authorization status.
    

Remember how we implemented permission verification in the initialization struct? The operation here is the same.

However, unlike in the initialization struct, in the ***Increment*** struct, we do not need to use a mutable annotation (`mut`) for the permission verification field. This is because, in the increment operation, we do not need to modify the state of the user's account; we only need to verify whether the user is authorized to perform the operation

**Syntax**

Signer, Struct

- hint
    
    ```rust
    #[derive(Accounts)]
    pub struct Increment<'info> {
        authority: Signer<'info>,
    }
    ```