# Content/super

In the previous lesson, we successfully defined a functional module, which is a key component of our ***Counter*** program.

Now, we face a new challenge: how to directly use the *structs and other elements* we defined earlier in this new module?

**Super Keyword**

```rust
super
```

In Rust, the `super` keyword represents *the parent module* of the *current module*. Therefore, we can use it to import all available items from the parent module. This includes previously defined **structs**, **enums**, **constants**, **type aliases**, **etc**.

**Syntax**

super

- hint
    
    ```rust
    pub mod demo {
        use super::*;
    }
    ```