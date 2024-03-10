# Content

In the previous section, we learned about the account attribute constraints within the accounts collection: `#[account(..)]`. In this section, we'll continue by studying the `#[account]` macro on data account structs. The positions of these two macros are different, as illustrated below:

```rust
#[derive(Accounts)]
pub struct InstructionAccounts {
		// Account attribute constraints
    #[account(init, seeds = [b"mySeeds"], payer = user, space = 8 + 8)]
    pub account_name: Account<'info, MyAccount >,
    ...
}

// #[account] macro on the account struct
#[account]
pub struct MyAccount {
    pub my_data: u64,
}
```

### **#[account]** Macro Introduction

In the Anchor framework, the `#[account]` macro is a special macro used for handling **(de)serialization**, **account discriminator**, and **ownership verification** of accounts. This macro significantly simplifies the development process, allowing developers to focus more on business logic rather than low-level account handling. It primarily implements the following traits:

- **(De)Serialization:** The Anchor framework automatically implements serialization and deserialization for structs marked with `#[account]`. This is because Solana accounts need to serialize data into byte arrays for transmission over the network, and the receiver needs to deserialize these byte arrays into appropriate data structures for processing.
- **Discriminator (Account Identifier):** It is an 8-byte unique identifier for the account type, derived from the SHA256 hash of the account type name's first 8 bytes. When implementing the account serialization trait, the first 8 bytes are reserved for the account discriminator. Therefore, during deserialization, the first 8 bytes of the incoming account are verified. If they don't match the definition, it is an invalid account, resulting in a failed account deserialization.
- **Owner (Ownership Verification):** The ownership of the Solana account corresponding to the struct marked with `#[account]` belongs to the program itself. It means that the ownership is declared in the program's **`declare_id!`** macro where the program ID is declared. In the code above, the ownership of the `MyAccount` is the program itself.

In summary, the `#[account]` macro syntax is simple, but the Anchor framework implements many functionalities under the hood, enhancing development efficiency.

Alright, that concludes the basic content of the Anchor framework. Next, let's explore some practical projects! 🚀🚀🚀

# Example

The complete program code is shown here.

```rust
//Introduce the pre-import module of the anchor framework
use anchor_lang::prelude::*;

//The on-chain address of the program
declare_id!("3Vg9yrVTKRjKL9QaBWsZq4w7UsePHAttuZDbrZK3G5pf");

//Instruction processing logic
#[program]
mod anchor_counter {
     use super::*;
     pub fn initialize(ctx: Context<InitializeAccounts>, instruction_data: u64) -> Result<()> {
         ctx.accounts.counter.count = instruction_data;
         Ok(())
     }

     pub fn increment(ctx: Context<UpdateAccounts>) -> Result<()> {
         let counter = &mut ctx.accounts.counter;
         msg!("Previous counter: {}", counter.count);
         counter.count = counter.count.checked_add(1).unwrap();
         msg!("Counter incremented. Current count: {}", counter.count);
         Ok(())
     }
}

//The set of accounts involved in the instruction
#[derive(Accounts)]
pub struct InitializeAccounts<'info> {
     #[account(init, seeds = [b"my_seed", user.key.to_bytes().as_ref()], payer = user, space = 8 + 8)]
     pub counter: Account<'info, Counter>,
     #[account(mut)]
     pub user: Signer<'info>,
     pub system_program: Program<'info, System>,
}

#[derive(Accounts)]
pub struct UpdateAccounts<'info> {
     #[account(mut)]
     pub counter: Account<'info, Counter>,
     pub user: Signer<'info>,
}

// Custom account type
#[account]
pub struct Counter {
     count: u64
}
```