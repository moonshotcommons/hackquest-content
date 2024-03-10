# Content/**Counter Instantiation and Assignment**

Continuing from our previous lesson, we have successfully created an instance of ***Counter***. Now, we need to assign this new instance to the previously obtained reference to the account ***counter***.

1. **Dereferencing**
    
    We use the dereferencing operation to update the data of the ***counter*** account.
    
    ```rust
    *counter = counter_instance;
    ```
    
    Here, the **`*`** is the dereferencing operator in Rust. Its functions are:
    
    - **Accessing the Data Pointed to by the Reference**: By dereferencing (***counter***), we are actually accessing and modifying the data of ***counter***, rather than just operating on a reference pointing to that data.
    - **Updating Account Data**: The assignment operation (`= counter_instance`) copies the data of our newly created ***Counter*** instance into ***counter*** . This means that the ***counter*** account now contains the updated data, such as the initial count value and the public key of the authorized user.

**Syntax**

counter dereferencing

- hint
    
    ```rust
    *counter = Counter {
                authority: *ctx.accounts.authority.key,
                count: 0,
                bump,
    };
    ```