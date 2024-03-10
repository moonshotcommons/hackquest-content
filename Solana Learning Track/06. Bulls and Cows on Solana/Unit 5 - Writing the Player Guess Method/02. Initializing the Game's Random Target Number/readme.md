# Content/**Defining the initialize Function**

In this section, we will use the previously learned ***generate_random_number*** *function* to generate a random target number for the game.

**Setting the Target Number**

```rust
pub fn initialize(ctx: Context<AccountContext>) -> Result<()> {
    let guessing_account = &mut ctx.accounts.guessing_account;
    guessing_account.number = generate_random_number();
    Ok(())
}
```

- `let guessing_account = &mut ctx.accounts.guessing_account;`: This line of code obtains a *mutable* reference  ***guessing_account***, allowing us to modify its state. This way, we can set the ***number*** parameter that ***guessing_account*** is supposed to record.
- `Ok(())`: Indicates that the initialization has been successfully completed and returns an empty tuple `()`.

**Syntax**

function

- hint
    
    ```rust
    pub fn my_function(ctx: Context<MyContext>) -> Result<()> {
        //......
        Ok(())
    }
    ```