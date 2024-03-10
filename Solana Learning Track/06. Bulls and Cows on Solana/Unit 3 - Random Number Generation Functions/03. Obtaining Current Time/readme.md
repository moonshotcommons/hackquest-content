# Content/**Getting Current Blockchain State Time Information**

In the previous lesson, we imported the ***Clock*** module from the Solana program library. In this lesson, we will use it to obtain the current time, which we will then use to generate a random number.

Now, we can use the ***Clock*** module we imported in the last lesson to get the current time information under the blockchain state:

```rust
fn generate_number() -> u32 {
	let clock = Clock::get().expect("Failed");	
}
```

- **Clock::get():** We call `Clock::get()` to obtain the ***Clock*** instance.
- **expect("Failed"):** If it fails to obtain, the program will stop and display *"Failed"*.

**Syntax**

function call

- hint
    
    ```rust
    fn generate_number() -> u32 {
    	let clock = Clock::get().expect("Failed");	
    }
    ```