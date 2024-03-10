# Content/**Adding the number Field**

In the last lesson, we defined a *struct* to store guesses. In this lesson, we will add a field to the struct for **recording the player's guesses**, which will later be used to determine if the guesses are correct.

**Adding the Field**

This *struct* will include a field to store the number.

```rust
#[account]
pub struct GuessingAccount {
    pub number: u32
}
```

**Syntax**

struct

- hint
    
    ```rust
    #[account]
    pub struct MyAccount {
        pub data: u32,
    }
    ```