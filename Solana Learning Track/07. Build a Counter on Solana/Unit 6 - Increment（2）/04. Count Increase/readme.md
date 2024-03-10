# Content/**Count Increase**

After passing the permission verification, our next task is to increase the value of the counter. This is the core functionality of the ***Counter*** program, allowing users to track and update the count value through program logic.

### **Specific Steps**

1. **Accessing the Counter**:
    
    We need to access the ***Counter*** account:
    
    ```rust
    ctx.accounts.counter
    ```
    
    Here, ***counter*** corresponds to the ***Counter*** account reference we defined earlier in the ***Increment*** struct.
    
2. **Modifying the Count Value**:
    
    Remember the ***count*** field on the ***Counter*** account? We set it to *0* during the initialization phase, and now we need to increase its value. A simple `+1` will do.
    

**Syntax**

+1

- hint
    
    ```rust
    ctx.accounts.counter.count += 1;
    ```