# Content/**Capturing User Input**

In our previous lessons, we learned how to capture user input and handle potential errors. However, now we face a new challenge: in a game, players often don't guess the correct answer on their first try. Therefore, we need to provide **multiple opportunities** for guessing.

To accommodate this, we will place the process within a *loop*, allowing players **multiple attempts** to guess until they find the correct answer.

### **Setting Up a Loop for Guessing**

In Rust, we can use the `loop` keyword to create an *infinite loop*, enabling players to make *multiple attempts* during the game.

```rust
loop {
			println!("Please input a number: ");
			let mut guess = String::new();
			io::stdin().read_line(&mut guess);
}
```

Within the *loop*, we will repeat the logic we learned earlier: obtaining input from the user and handling errors.

**Syntax**

loop

- hint
    
    ```rust
    loop {
        // loop code
    }
    ```