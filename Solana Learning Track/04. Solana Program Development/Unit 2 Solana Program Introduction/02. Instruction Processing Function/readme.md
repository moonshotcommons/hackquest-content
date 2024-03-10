# Content

Learning Objective: Understand the instruction processing function `process_instruction`.

Recall that Solana program accounts only store the logic for processing instructions. This means program accounts are "read-only" and "stateless." The "state" (data set) required for program instruction processing is stored in data accounts (separate from program accounts).

### Definition of Data Account

To implement the accumulation of a counter in our Solana program, we must first define how this data is stored on the Solana. Here, we use the `CounterAccount` struct. The use of the "Account" suffix signifies that it is a data account (initially confusing for developers transitioning from Ethereum, but it becomes clear over time as a clever design).

```rust
/// Definition of the structure for a data account
#[derive(BorshSerialize, BorshDeserialize, Debug)]
pub struct CounterAccount {
    pub count: u32,
}
```

In this struct, we define a property `count` of type `u32`. This value increments by 1 each time a transaction instruction is initiated. As the value is stored and transmitted using bytecode, we need (de)serialization operations, and here we introduce the `borsh` library.

```rust
use borsh::{BorshDeserialize, BorshSerialize};
```

The actual (de)serialization operations are implemented through the `BorshSerialize` and `BorshDeserialize` derive macros. The macros' definitions process metadata of Rust code represented as `TokenStream` and return the processed metadata.

```rust
#[proc_macro_derive(BorshSerialize, attributes(borsh_skip))]
pub fn borsh_serialize(input: TokenStream) -> TokenStream {
    // Serialization logic...
}

#[proc_macro_derive(BorshDeserialize, attributes(borsh_skip, borsh_init))]
pub fn borsh_deserialize(input: TokenStream) -> TokenStream {
    // Deserialization logic...
}
```

### Instruction Processing Function

The definition of this function has been introduced earlier. Here, we examine its implementation logic.

```rust
pub fn process_instruction(
    // Program ID, i.e., program address
    program_id: &Pubkey,
    // Collection of accounts involved in this instruction
    accounts: &[AccountInfo]) -> ProgramResult 
{

    // Iterator for accounts
    let accounts_iter = &mut accounts.iter();

    // Get the caller's account
    let account = next_account_info(accounts_iter)?;

    // ...
}
```

To process an instruction, the data account required for the instruction must be explicitly passed into the program through the `accounts` parameter. As we are performing an operation to accumulate the data account, the `accounts` include this data account, and we obtain it through the iterator as `account`.

The `account` data account is derived from this program, making the current program its `owner`. Only the owner can perform write operations on it. Therefore, we need to verify the account's ownership.

```rust
// Validate the caller's identity
if account.owner != program_id {
    msg!("Counter account does not have the correct program id");
    return Err(ProgramError::IncorrectProgramId);
}
```

# Example

The complete instruction processing function code is as follows:

```jsx
pub fn process_instruction(
		 //Program ID, that is, program address
     program_id: &Pubkey,
		 //The set of accounts involved in this command
     accounts: &[AccountInfo],
		 // command data
     _instruction_data: &[u8],
) -> ProgramResult {
     msg!("Hello World Rust program entrypoint");

     //Account iterator
     let accounts_iter = &mut accounts.iter();

     // Get the caller account
     let account = next_account_info(accounts_iter)?;

     //Verify caller identity
     if account.owner != program_id {
         msg!("Counter account does not have the correct program id");
         return Err(ProgramError::IncorrectProgramId);
     }

     // Read and write new values
     let mut counter = CounterAccount::try_from_slice(&account.data.borrow())?;
     counter.count += 1;
     counter.serialize(&mut *account.data.borrow_mut())?;

     Ok(())
}
```