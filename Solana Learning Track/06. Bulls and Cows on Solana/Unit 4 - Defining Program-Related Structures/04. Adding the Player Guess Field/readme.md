# Content/**Adding the guessing_account Field**

In the last lesson, we defined a *program account struct* to manage account states during program interactions. In this lesson, we will add a field to the struct for *passing the player's guesses*.

**Adding the Field**

Next, we add a field named ***guessing_account*** to the ***AccountContext***.

```rust
#[derive(Accounts)]
pub struct AccountContext<'info> {
    #[account(
        init_if_needed,
        space=32,
        payer=payer,
        seeds = [b"guessing pda"],
        bump
    )]
    pub guessing_account: Account<'info, GuessingAccount>,
}
```

`guessing_account: Account<'info, GuessingAccount>`：

- `'info`: A lifetime parameter, ensuring this account reference is valid throughout the entire ***AccountContext*** struct's lifetime.
- `GuessingAccount`: The type parameter we learned about in the last lesson, specifies the *data type* this account will hold.

Here we also use the `#[account]` macro to configure various properties of  ***guessing_account***, such as **initialization** method, **space size**, and **payer account**.

1. `init_if_needed`: Instruct the Anchor to automatically *initialize* the account when needed. If the account is not yet *initialized*, Anchor will *initialize* it based on other *provided parameters* (like ***space*** and ***payer***).
2. `space=32`: The storage space size needed for the account data, *32* bytes, which should be sufficient to hold all data in the ***GuessingAccount***.
3. `payer=payer`: Specifies the payer account.
4. `seeds = [b"guessing pda"], bump`: Used to generate a **Program Derived Address (PDA)**.

**Syntax**

struct

- hint
    
    ```rust
    #[derive(Accounts)]
    pub struct MyContext<'a> {
        pub my_account: Account<'a, MyAccount>,
    }
    ```