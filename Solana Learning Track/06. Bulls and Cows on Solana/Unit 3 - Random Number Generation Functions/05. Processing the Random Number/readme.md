# Content/**Processing the Random Number**

In the previous lesson, we obtained the current timestamp from the Solana program library and generated a random number. In this lesson, we will continue to *process* this random number.

**Processing the Random Number**

To ensure the random number is not *0* and is within the range of *1* to *10*, we add *1* to the obtained number:

```rust
fn generate_random_number() -> u32 {
     let clock = Clock::get().expect("Failed to get clock");
     let last_digit = (clock.unix_timestamp % 10) as u8;
     let result = (last_digit + 1) as u32;
     result
}
```

We convert it to `u32` type and return it. This way, we obtain a random number between *1* to *10*.

**Syntax**

as: Type conversion.

- hint
    
    ```rust
    let result = (last_digit + 1) as u32;
    ```