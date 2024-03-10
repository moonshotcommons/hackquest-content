# Content/**Converting and Processing User Input**

In the previous lesson, we learned how to use the ***trim*** method to remove unnecessary whitespace from user input. In this lesson, we will learn how to ***convert*** the captured string into a numerical type and ***process*** the conversion result for subsequent logical judgments and calculations.

### **Using parse to Convert Strings**

In the last lesson, we used the ***trim*** method to process the input string.

```rust
let guess = guess.trim()；
```

We then call the ***parse*** method, specifying the type to convert to. In this example, we attempt to convert the `string` into a `u32` type integer:

```rust
let guess: u32 = match guess.trim().parse() {
					
		Ok(num) => num,
		Err(_) => {
		    println!("Please input valid number");
		    continue;
		}
};
```

- **let guess: u32 = match guess.trim().parse() { ... }**: This line of code attempts to parse the whitespace-trimmed string into a `u32` type integer, so we declare the original ***guess*** variable as a `u32` integer type.
- **match**: Since the ***parse*** method's conversion of the `string` to an `integer` type might succeed or fail, we use a `match` expression to handle each possible outcome (`Ok` and `Err`).
- **Ok(num) => num**: If ***parse*** is successful, the *Result* will be `Ok(num)`, where ***num*** is the parsed number. Here, we use **`=>`** to directly return the parsed integer ***num*** .
- **Err(_) => {...}**: If ***parse*** fails, the *Result* will be `Err(_)`, where **`_`** is a wildcard representing any error. We output an error message and use `continue` to skip the current loop iteration, prompting the user to re-enter.

**Syntax**

String parse

match

Result

- hint
    
    ```rust
    let number: u32 = match text.trim().parse() {
    					
    		Ok(num) => num,
    		Err(_) => {
    		    println!("Please input valid number");
    		    continue;
    		}
    };
    ```
    