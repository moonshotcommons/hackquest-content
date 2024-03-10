# Content/**Introducing the io Library**

After our previous lessons where we successfully generated random numbers and recorded the number of player attempts, this section will focus on capturing user input, a key step in making the game *interactive*. First, we need to introduce the ***io*** (input/output) module from Rust's standard library.

### **Introducing the *std::io* Library**

To read user input from the terminal, we need to use the ***std::io*** module. This module provides various functionalities for **handling input and output**, and we will use it to read the numbers input by users.

> At the beginning of the program, we need to use the `use` statement to import `std::io`. This allows us to directly use io-related functions in the main body of our program.
> 

```rust
use std::io;
```

For our game, the most crucial is the ***stdin*** function in the ***std::io*** module, which we can use to read data input by users.

**Syntax**

**use**

- hint
    
    ```rust
    use rand::Rng;
    ```
    