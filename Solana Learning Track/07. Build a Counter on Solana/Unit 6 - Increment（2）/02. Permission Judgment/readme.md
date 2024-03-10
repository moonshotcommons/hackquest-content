# Content/**Permission Judgment**

In the previous section, we successfully defined the header of the ***increment*** function and clarified its accessibility and return type. Now, we will start implementing the key logic inside the *function*, starting with permission judgment.

### **Implementing Permission Judgment**

1. **Using the require_keys_eq! Macro for Comparison**:
    
    At the beginning of the *function*, we first need to ensure that the user calling this *function* has the appropriate permissions. For this, we can use the `require_keys_eq!` macro. This macro will help us verify whether the caller is the authorized user.
    
    <aside>
    💡 The `require_keys_eq!` macro compares two public key parameters. If these two public keys are equal, the macro does nothing, and the program continues to execute. If they are not equal, it triggers an error.
    
    </aside>
    
2. **Handling Permission Verification Failure**:
    
    If the two public keys compared in the macro do not match, meaning the user performing the operation does not have the appropriate permissions, we need to notify the caller. In this case, we return an `ErrorCode::Unauthorized` error. (We will explain this error in detail in the next lesson)
    
    ```rust
    require_keys_eq!(key1, key2, error_code);
    ```
    

Such error handling ensures that only *correctly authorized users* can change the value of the counter, enhancing the security of the on-chain program.

**Syntax**

require_keys_eq!

- hint
    
    ```rust
    require_keys_eq!(
                ctx.accounts.authority.key(),
                ctx.accounts.counter.authority,
                ErrorCode::Unauthorized
            );
    ```