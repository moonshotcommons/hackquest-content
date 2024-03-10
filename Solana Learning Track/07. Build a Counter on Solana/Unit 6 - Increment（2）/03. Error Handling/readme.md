# Content/**Error Handling**

Continuing from the previous lesson, when using the `require_keys_eq!` macro for permission verification, if the public keys do not match, an error code is returned. Next, let's look at how to define errors.

### **Error Code Enumeration (ErrorCode Enum)**

Error handling is an important part of programs. The `ErrorCode` enumeration allows us to define a range of possible error scenarios and specify a clear message for each error.

### **Defining the ErrorCode Enumeration**

1. **Using the #[error_code] Attribute**:
    
    `#[error_code]` is an attribute used to mark `ErrorCode` as an enumeration for defining error codes. This attribute associates each variant of `ErrorCode` with a specific error scenario.
    
2. **Defining Different Types of Errors**:
    
    In the `ErrorCode` enumeration, we can define various types of errors. Each type represents a specific error that might occur during the execution of the program.
    

```rust
#[error_code]
pub enum ErrorCode {
    #[msg("The requested operation is not permitted.")]
    OperationNotAllowed,

    #[msg("The provided input is invalid.")]
    InvalidInput,

    #[msg("Insufficient funds to perform the operation.")]
    InsufficientFunds,

    // More error types...
}
```

Here:

- `#[msg("...")]`: The attribute before each error type is used to define the specific error message returned to the user when that error is triggered.
- Enumeration variables: Such as  ***OperationNotAllowed***、***InvalidInput***, and ***InsufficientFunds***, these are custom error types that can be defined according to the specific needs of the program.

Therefore, we need to define an unauthorized error type to be used in the `require_keys_eq!` macro for permission judgment.

**Syntax**

ErrorCode 

- hint
    
    ```rust
    #[error_code]
    pub enum ErrorCode {
        #[msg(".....")]
        Unauthorized,
    }
    ```