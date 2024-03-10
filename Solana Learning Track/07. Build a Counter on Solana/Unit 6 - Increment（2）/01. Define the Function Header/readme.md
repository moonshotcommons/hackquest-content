# Content/Define the function header

In the previous chapters, we have successfully defined an ***Increment*** struct. Now, we begin writing the core *function* of the program, ***Increment***.

First, we need to define the function header in the functional module.

### **Defining increment**

1. **Declare the Function**:
    - We want this function to be public, meaning it can be called by users outside the program or by other programs.
    - We want the function to have access to all the data defined in the `Increment` struct, so we need to pass the corresponding context as a parameter.
2. **Specify the Return Type**:
    
    Although we strive to perfect our code and minimize errors, the function might return success (`Ok(())`) or encounter an error (`Err(...)`). Therefore, we can return a `()`, which indicates that our function does not return any additional values upon success.
    

**Syntax**

function

- hint
    
    ```rust
    pub fn increment(ctx: Context<Increment>) -> Result<()> {
        
    }
    ```