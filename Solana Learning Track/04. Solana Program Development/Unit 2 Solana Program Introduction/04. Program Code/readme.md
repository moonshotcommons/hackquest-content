# Content

Through the analysis of various sections of the program in the previous sections, let's now take a look at the complete counter program.

The complete code is on the right, and it includes the following aspects we discussed earlier:

- Introducing dependencies: `borsh` and `solana_program`
- Definition of the data account
- Declaration of the program entry point function
- Core logic of the program: the instruction processing function

<aside>
💡 In summary, in this Solana-based program, we need to implement operations such as (de)serialization, specifying the program entry point, and account security checks. While these are necessary for program development, they can be cumbersome. If you use the Anchor framework, you can be freed from these repetitive tasks and focus more on the core business logic of the program. In the subsequent chapters, we will specifically introduce the Anchor development framework for Solana.

</aside>

# Example

Here is a counter program implemented in Solana.

```rust
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