# Content/**Defining the AccountContext Struct**

In this lesson, we will learn how to define a *program account struct*, which is used to *manage account states* during the execution of a smart contract.

**Creating the Struct**

The ***AccountContext*** struct will contain all necessary account references needed for the execution of the smart contract.

 First, we define the struct and use the `#[derive(Accounts)]` macro.

```rust
#[derive(Accounts)]
pub struct AccountContext<'info> {
    // Fields will be defined here
}
```

`#[derive(Accounts)]`: Transforms the struct into a *type* corresponding to *blockchain accounts*, used for storing and manipulating game states;

`<'info>`： A lifetime parameter, specifying the *validity period* of references within the struct.

**Syntax**

struct

- hint
    
    ```rust
    #[derive(Accounts)]
    pub struct MyContext<'a> {
        pub my_account: Account<'a, MyAccount>,
    }
    ```