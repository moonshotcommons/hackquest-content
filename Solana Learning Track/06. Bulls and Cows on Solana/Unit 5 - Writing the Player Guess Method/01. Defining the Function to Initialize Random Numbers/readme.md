# Content/**Defining the initialize Function**

In this lesson, we will learn how to define a function for initializing random numbers. This function will be responsible for initializing our random number and recording it.

**Creating the Function:**

```rust
pub fn initialize(ctx: Context<AccountContext>) -> Result<()> {
    // The function body will be implemented here
}
```

- ***ctx***: Accepts a parameter of type `Context<AccountContext>`, representing the current program context.
- ***Result<()>***: Returns a `Result` type, where `()` indicates that no value is returned on success, while an error situation will return `Err`.

**Syntax**

function

- hint
    
    ```rust
    pub fn my_function(ctx: Context<MyContext>) -> Result<()> {
        //......
        Ok(())
    }
    ```
    