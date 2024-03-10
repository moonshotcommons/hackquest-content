# Content/Receiving Parameter Information

In the previous section, we defined the ***initialize** function* and passed the ***Initialize*** struct as a *parameter*. This struct contains all the key information needed for the initialization process, such as the *authorized user* and the *counter account*. Now, we will explain in detail how to handle these passed *parameters* in the function.

### **Specific Steps**

- **Receiving and Modifying the Counter Account's Information**:
    
    Our goal is to read and update the data of the ***Counter*** account. To achieve this, we first need to obtain a mutable reference to the account. This can be done using the `deref_mut()` method.
    
    ```rust
    ctx.accounts.counter.deref_mut()
    ```
    
    `ctx.accounts.counter` provides access to the ***Counter*** account. By using the `deref_mut()` method, we obtain a mutable reference, meaning we can now read and modify the data of the ***Counter*** account.
    
    > For example, we might need to initialize the counter's value or set the authorized user.
    > 

**Syntax**

deref_mut()

- hint
    
    ```rust
    let counter = ctx.accounts.counter.deref_mut()
    ```