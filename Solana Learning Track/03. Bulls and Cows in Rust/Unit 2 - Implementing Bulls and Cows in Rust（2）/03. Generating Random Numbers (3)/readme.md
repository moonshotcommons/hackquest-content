# Content/**Tracking Attempt Counts**

After learning how to generate random numbers using the ***rand*** library in the previous lesson, in this section, we will further enhance our ***Bulls and Cows*** game by adding an *integer* variable to track the number of guesses made by the player.

### **Adding Record of Attempt Counts**

In the game, tracking the number of attempts a player makes is an important feature. It not only serves to display the player's current progress but also helps determine when the game ends.

```rust
let mut attempts = 0;
```

- Declare a *mutable* variable ***attempts***: In Rust, *mutable* variables allow us to change their *values* during their lifetime. For the attribute of recording the number of player attempts, it needs to be defined as a *mutable* variable because we need to *update* this count each time the player makes a guess.
- Initialize the Variable: Initialize the ***attempts*** variable to *0*, indicating that at the start of the game, the player has not made any attempts yet.

In short, this line of code declares a *mutable* variable named ***attempts*** and *initializes* it to *0*.

**Syntax**

**Mutability**

- hint
    
    ```rust
    let mut number = 0;
    ```
    