# Content/**Data Preprocessing**

In our previous lessons, we learned how to capture user input data. Next, we will explore how to **preprocess** this captured data to ensure its accuracy and usability.

In this section, we will use the *trim* method to remove unnecessary *whitespace characters* from user input.

### **Removing Whitespace Characters**

When users input data, they might accidentally include *spaces or newline characters* at the beginning or end. These extra whitespace characters can interfere with the logical processing of our program. Therefore, we use the trim method to eliminate these unwanted characters.

```rust
let input_data = "   42   ";
let trimmed_data = input_data.trim();

println!("Original Data: '{}'", input_data); //"   42   "
println!("Trimmed Data: '{}'", trimmed_data);//"42";
```

This line of code removes all whitespace characters from both ends of the ***input_data*** string and stores the result in a new variable  ***trimmed_data***.

**Syntax**

String

trim

- hint
    
    ```rust
    let trimmed = text.trim();
    ```