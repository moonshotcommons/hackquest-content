# Content/**Capturing User Input**

From our previous lesson, we learned how to introduce the ***std::io*** module, preparing us to capture user input for our program. Now, let's learn how to use this ***io*** module to read numbers entered by users in the terminal.

### **Creating a Variable to Store User Input**

To store the data input by users, we need a variable. This variable should be *mutable*, as users may input data multiple times, causing the variable's value to change.

```rust
let mut input_data = String::new();
```

- String::new(): Creates a new empty string, serving as a container for storing user input data.
- let mut input_data: Declares a *mutable string* variable named ***input_data*** and *initializes* it as an empty string with `String::new()`.

### **Reading User Input**

Next, we use the ***stdin*** function from the ***std::io*** module to read the user's input.

```rust
io::stdin().read_line(&mut input_data);
```

- io::stdin(): Used to capture input from users in the *terminal*. It provides a channel that allows the program to receive data input by users via the keyboard. Simply put, it acts like a bridge connecting the user's keyboard to your program.
- read_line(&mut input_data): Reads the text input by the user and *stores* it in the **specified** variable. This method requires a *mutable* reference to a variable so that it can save the captured input into that variable.

In essence, this line of code uses the ***stdin()*** function to obtain a handle for terminal input and calls the ***read_line*** method to write the data input by the user into the previously created ***input_data*** string.

**Syntax**

Mutable Variable

String

Function Call

- hint
    
    ```rust
    let mut number = 1;
    let mut str = String::new();
    rand::thread_rng().gen_range(1..11);
    ```
    