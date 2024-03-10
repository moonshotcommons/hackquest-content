# Content

Introduction: Through the previous chapters, we have gained a certain understanding of the basic concepts of `Solana` and the foundational syntax of `Rust`. ***Now, let's implement a simple counter program on Solana to grasp the complete development process in Solana through this small demo***.

### Program Overview

***This program implements the functionality of incrementing a counter, meaning that each time the program is called, the internal counter increases by 1***. While it is a simple feature, it covers the following topics we have previously learned:

- Rust basic data types, arrays, structs, etc.
- Rust functions and error handling
- Rust module system
- Rust function-like macro and derived macro
- Solana account
- Solana program, transaction, instruction
- Solana browser-based IDE: ***Playground***
- Solana program compilation, deployment, testing
- Solana blockchain explorer
- ...

> The complete code is on the right. If you feel confused, it's okay; in the following chapters, we will step by step provide explanations.
> 

### Course Outline:

1. Rust Module System
2. Rust Functions
3. Rust Result & Enum
4. Solana Program Dependencies
5. Solana Program Entry Point
6. Solana Instruction Processing Function
7. Return Values of Solana Instruction Functions
8. Building and Deploying on Solana
9. Solana Browser Exploration

# Example

```jsx
use borsh::{BorshDeserialize, BorshSerialize};
use solana_program::{
     account_info::{next_account_info, AccountInfo},
     entrypoint,
     entrypoint::ProgramResult,
     msg,
     program_error::ProgramError,
     pubkey::Pubkey,
};

/// Define the structure of the data account
#[derive(BorshSerialize, BorshDeserialize, Debug)]
pub struct CounterAccount {
     pub count: u32,
}

//Define program entry point function
entrypoint!(process_instruction);

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