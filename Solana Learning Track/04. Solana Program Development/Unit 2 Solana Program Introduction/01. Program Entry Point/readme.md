# Content

Learning Objectives: Master the concepts of the `solana_program` library crate and the program entry point `entrypoint`.

Recall that all data stored on the Solana network is contained within entities called accounts. Each account has its unique address for identification and access to the account data. A Solana program is a specific type of Solana account used for storing and executing instructions.

### **Solana crate** solana_program

To write Solana programs in Rust, we need to use the standard library for Solana programs, `solana_program`. This library includes modules and macros that we'll use for developing Solana programs. For a deeper understanding of the `solana_program` crate, refer to the **[solana_program crate documentation](https://docs.rs/solana-program/latest/solana_program/index.html)**.

For a basic program, we need to bring the following items from the `solana_program` library into scope:

```rust
use solana_program::{
    account_info::AccountInfo,
    entrypoint,
    entrypoint::ProgramResult,
    pubkey::Pubkey,
    msg
};
```

- `AccountInfo`: A struct from the `account_info` module allowing us to access account information.
- `entrypoint`: A macro for declaring the program entry point, similar to the `main` function in Rust.
- `ProgramResult`: The return value type from the `entrypoint` module.
- `Pubkey`: A struct from the `pubkey` module allowing us to access addresses as public keys.
- `msg`: A macro allowing us to print messages to the program log, similar to Rust's `println` macro.

### **Solana Program Entry Point**

A Solana program requires a single entry point to handle program instructions. The entry point is declared using the `entrypoint!` macro.

Declare the program's entry point function as follows:

```rust
entrypoint!(process_instruction);
```

The instruction processing function has been introduced in the previous sections and is not reiterated here.

```rust
fn process_instruction(
    // Current program ID
    program_id: &Pubkey,
    // Collection of accounts involved in this instruction
    accounts: &[AccountInfo],
    // Parameters for this instruction
    instruction_data: &[u8],
) -> ProgramResult;
```