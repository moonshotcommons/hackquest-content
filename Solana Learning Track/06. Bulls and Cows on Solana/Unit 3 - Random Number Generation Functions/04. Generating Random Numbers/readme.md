# Content/**Obtaining Timestamp**

In the previous lesson, we obtained the current time information from the Solana program library. Now, we will continue to learn how to use this information to generate a simple random number.

**Obtaining the Last Digit of the Current Timestamp**

We will use the ***Clock*** instance to get the timestamp representing the current time and then take the *last digit of the timestamp* as our generated random number:

```rust
fn generate_random_number() -> u32 {
	let clock = Clock::get().expect("Failed to get clock");
	let last_digit = (clock.unix_timestamp % 10) as u8;
}
```

We obtain the last digit of the current timestamp by taking the modulo (`%10`) of the timestamp and then convert it to `u8` type.

- **unix_timestamp**: UNIX timestamp.

**Syntax**

**%:** Modulo operation

- hint
    
    ```rust
    let last_digit = (clock.unix_timestamp % 10) as u8;
    ```