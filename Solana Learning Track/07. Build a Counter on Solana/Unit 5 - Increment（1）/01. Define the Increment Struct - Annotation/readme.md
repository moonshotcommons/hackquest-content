# Content/Annotation

After completing the initialization operation in the previous lessons, next, we will focus on implementing the core functionality of our on-chain programs—*increment*, which is to increase the value of the *counter*.

To achieve this functionality, we need to define a *dedicated struct* to organize and receive the information required for executing the increment operation. Similar to the initialization process, the increment operation also involves interactions with multiple accounts. Therefore, we will use the `#[derive(Accounts)]` macro to manage these accounts and operations.

Remember how we defined the initialization struct previously? Let's mimic that to define the increment struct.

**Syntax**

#[derive(Accounts)]，<'info> ，Struct

- hint
    
    ```rust
    #[derive(Accounts)]
    pub struct Increment<'info> {
    }
    ```