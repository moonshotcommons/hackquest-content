# Content/Writing Functional Functions

Great, in the previous lessons, we have already defined the *data structure* and *initialization logic* of ***Counter***. Now, we are moving into a new phase: starting to write the functional *functions* of the *program*.

### **Creating a Functional Module**

To organize and implement our program's functionalities, we first need to *create a functional module*. This module will contain all the functions that define the program's behavior. In Rust, we organize these functions by defining a module:

```rust
pub mod demo {
}
```

Since it's the core functional part, we can use the `#[program]` annotation. This annotation is akin to telling the compiler: 'The following section of code is the core of the program, containing all its operations and methods.

**Syntax**

mod

- hint
    
    ```rust
    #[program]
    pub mod demo {
        // functions
    }
    ```