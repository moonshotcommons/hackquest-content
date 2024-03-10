# Content

Learning Objective: Understand the instruction processing function `process_instruction`.

In this section, we continue to explore the read and write operations in the instruction function.

### Reading Data Account

After the account ownership validation in the previous section, we can be confident that the current data account is correct. The next step is to read the data stored in this account.

```rust
let mut counter = CounterAccount::try_from_slice(&account.data.borrow())?;
```

The purpose of this line is to deserialize an instance of the `CounterAccount` struct from the Solana data account.

1. `&account.data`: Obtain a reference to the data field of the account. In Solana, the data field of an account (`data`) stores the actual data associated with the account. For a program account, it is the binary content of the program. For a data account, it is the stored data.
2. `borrow()`: Use this method to obtain a borrowable reference to the `data` field. Through `&account.data.borrow()`, we get a reference to the account's data field.
3. `CounterAccount::try_from_slice(...)`: Call the `try_from_slice` method, which is a method of the `BorshDeserialize` trait, used to deserialize an instance of a struct from a byte sequence. Here, `CounterAccount` implements `BorshDeserialize`, enabling the use of this method.
4. `?`: This is an error-handling operator. If `try_from_slice` returns an error, the entire expression will return early, propagating the error to the caller.

In this way, we obtain a deserialized instance of the `CounterAccount` data account and acquire its mutable borrow.

### Modifying Data Account

Now, we can modify this data account:

```rust
counter.count += 1;
counter.serialize(&mut *account.data.borrow_mut())?;
```

- Increment the `count` field in the `CounterAccount` struct.
- `&mut *account.data.borrow_mut()`: Use `borrow_mut()` to obtain a mutable reference to the account's data field. Then, use `*` dereferencing to get the value of this `data` field and convert it to a mutable reference with `&mut`.
- `serialize` function method: This is a method of the `BorshSerialize` trait, used to serialize a struct into a byte array.
- `?`: This is an error-handling operator. If the `serialize` method returns an error, the entire expression will return early, propagating the error to the caller.

With these steps, we increment the modified value in the `CounterAccount` struct and serialize the updated struct into a byte array, then write it into the mutable data field of the Solana account. This achieves the update and storage of the counter value in a Solana program.

# Example

The complete `process_instruction` function code is as follows:

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

# **Button/Try it out**

[https://beta.solpg.io](https://beta.solpg.io/)