# Content

Learning Objectives: Understand the Result return type in Rust and the Program type in Solana.

In the Rust Basics course, we introduced the Result type in Chapter 6.1, "Error Handling." Let's briefly review.

### Result Enum

`Result` is a standard library type that represents two different outcomes: success (`Ok`) or failure (`Err`). When using `Ok` or `Err`, you must include a value, and the type of that value is determined by the context of the code. For example, a function with a return type of `Result<String, i64>` indicates that the function can return an `Ok` with a `String` or an `Err` with an `i64` integer. In this example, the integer serves as an error code that can be used for proper error handling.

To return a success case with a `String`, you can do:

```rust
Ok(String::from("Success!"));
```

To return an error with an integer, you can do:

```rust
Err(404);
```

### ProgramResult Enum

`ProgramResult` is a generic error handling type defined in Solana. It is a struct in the `solana_program` crate, as shown below:

```rust
use solana_program::entrypoint::ProgramResult;
```

It represents the return value of the instruction processing function in a Solana program. This type represents the result of processing an instruction in a transaction. On success, it returns the unit type `()`, indicating an empty return value. On failure, it returns `ProgramError`, which is itself an enum.

```rust
use std::result::Result as ResultGeneric;

pub type ProgramResult = ResultGeneric<(), ProgramError>;
```

Within `ProgramError`, there are 23 common error reason enum values defined, and it also supports custom error types. Here is an example:

```rust
pub enum ProgramError {
    #[error("Custom program error: {0:#x}")]
    Custom(u32),

    #[error("The arguments provided to a program instruction were invalid")]
    InvalidArgument,

    #[error("An instruction's data contents were invalid")]
    InvalidInstructionData,

    #[error("An account's data contents were invalid")]
    InvalidAccountData,

    // ...
}
```