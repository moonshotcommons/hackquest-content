# Content/Attribute Declaration

In the previous section, we successfully defined the framework of the ***Increment*** struct. Now, our task is to specifically fill this struct to ensure we can execute the increment operation.

To implement the increment functionality, we need to focus on two main aspects:

1. **Accessing the Counter**: 
    
    First, we need direct access to and the ability to modify the counter's value. This means our struct should include a reference to the ***Counter*** account.
    

<aside>
💡 This will allow us to read the current count value and update it according to the increment operation.

</aside>

1. **Permission Verification (this part will be covered in the next section)**

Remember how we implemented the reference to the counter account in the initialization struct?

- Initialize
    
    ```rust
    #[derive(Accounts)]
    pub struct Initialize<'info> {
        #[account(
            init,
            payer = authority,
            space = Counter::SIZE,
            seeds = [b"counter"],
            bump
        )]
        counter: Account<'info, Counter>,
    }
    ```
    

Similar to this, but with slightly different attribute configurations. After initialization, we only need to focus on two points:

- We must ensure that we can modify the count value within the ***Counter***  account, which can be done using the `mut` keyword.
- We must ensure precise identification of the specific ***Counter***  account previously created and initialized, which can be achieved by specifying the PDA (Program Derived Address) using the `seeds` and `bump` parameters.
    
    ```rust
    seeds = [b"counter"],
    bump = counter.bump
    ```
    

**Syntax**

#[account(…)]，Struct

- hint
    
    ```rust
    #[derive(Accounts)]
    pub struct Increment<'info> {
        #[account(
            mut,
            seeds = [b"counter"],
            bump = counter.bump
        )]
        counter: Account<'info, Counter>,
    }
    ```