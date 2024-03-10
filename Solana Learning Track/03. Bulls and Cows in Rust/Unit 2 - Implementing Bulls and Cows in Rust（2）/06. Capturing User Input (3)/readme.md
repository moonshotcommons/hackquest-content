# Content/**Handling Input Exceptions**

After learning how to *read* user input data in the last lesson, we now face the possibility of encountering *errors* in this process. Therefore, in this lesson, we will focus on how to handle potential input errors.

### **Understanding the Return Value of *read_line***

```rust
io::stdin().read_line(&mut guess);
```

We previously learned to use the ***read_line()*** method from ***io.stdin()*** to read values entered by users in the command line.

> The ***read_line()*** method might face various issues while reading input, such as *illegal characters* entered by the user or *interruptions* during the input process.
> 

The ***read_line()*** method returns a value of the `Result` type, an enumeration that can be either *Ok* or *Err*.

- **Ok**: Indicates successful operation, containing the number of bytes successfully read.
- **Err**: Indicates a failed operation, containing error information.

### **Handling Errors with expect**

To manage potential errors, we use the ***expect*** method. If the ***read_line*** method returns an *Err* value, expect will stop the program and display the error message you provide, aiding in quick error identification and resolution.

```rust
io::stdin().read_line(&mut guess).expect("Failed to read line");
```

By adding `.expect("Failed to read line")` after the ***read_line*** call, if an error occurs while reading the input, the program will stop running and display *"Failed to read line"*.

**Syntax**

**Error Handling with expect**

- hint
    
    ```rust
    .expect("error message");
    ```
    