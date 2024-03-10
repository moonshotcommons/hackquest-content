# Content/**Importing Clock Dependency**

As mentioned in the previous lesson, we will use the Solana program library to obtain the current time and then use this time to generate a random number. In this lesson, we will learn how to *import* the Solana program library that provides the current time.

**Importing the Clock Dependency**

In Solana development, if we want to obtain the current timestamp, we need to use the ***Clock*** module from the Solana program library:

```rust
use solana_program::clock::Clock;
```

This line of code imports the ***Clock*** module from the Solana program library, through which we can obtain the current time on the blockchain.

> Time Information: The ***Clock*** module provides the current *UNIX timestamp*, which is the number of seconds since **January 1, 1970**.
> 

> Security: Although the ***Clock*** module can conveniently provide current time information, the time it provides is **the result of blockchain node consensus** and not an absolutely accurate global time source. Therefore, logic that relies on time may be susceptible to manipulation by malicious actors who exploit time manipulation for attacks. (In this course, we use the ***Clock*** to implement a simple random number generation example for ease of understanding.)
> 

**Syntax**

use

- hint
    
    ```rust
    use getrandom::getrandom;
    ```