# Content

In the previous section, we provided an overall introduction to the macros in the Anchor framework. In this section, we will continue our exploration with the `#[program]` macro.

```rust
#[program]
mod program_module_name {
    // ...
}
```

### #[program] Macro

This macro defines a Solana program module containing the program's instructions and other related logic. It encompasses the following functionalities:

**1. Definition of Functions Handling Different Instructions:**
Within the program module, developers can define functions that handle different instructions. These functions encapsulate the specific logic for processing instructions. In the previous section, we had only one instruction function, `instruction_one`. In this section, within the #[program] macro, we implement two instruction functions: `initialize` and `increment`, designed to implement logic related to a counter, making it closer to real-world business scenarios.

```rust
#[program]
mod anchor_counter {
    use super::*;

    // Initialize the account with the provided instruction_data as the initial value of the counter
    pub fn initialize(ctx: Context<InitializeAccounts>, instruction_data: u64) -> Result<()> {
        ctx.accounts.counter.count = instruction_data;
        Ok(())
    }

    // Increment the counter by 1 based on the initial value
    pub fn increment(ctx: Context<UpdateAccounts>) -> Result<()> {
        let counter = &mut ctx.accounts.counter;
        msg!("Previous counter: {}", counter.count);
        counter.count = counter.count.checked_add(1).unwrap();
        msg!("Counter incremented. Current count: {}", counter.count);
        Ok(())
    }
}
```

**2. Interaction with Solana SDK:**
Through the `#[program]` macro, the Anchor framework provides functionalities to simplify interaction with the Solana SDK. For instance, you can directly use structures and macros such as `declare_id`, `Account`, `Context`, `Sysvar`, etc., without manually writing low-level Solana interaction code. In the first section of this unit, where we didn't use the Anchor framework, manual iteration over accounts and checking account permissions were required. Now, Anchor has implemented these functionalities for us.

**3. Automatic Generation of Interface Definition Language (IDL):**
The `#[program]` macro is also used for the automatic generation of the program's Interface Definition Language (IDL). IDL is a specification used to describe the interface of a Solana program, defining data structures, instructions, etc. The Anchor framework uses this information to generate Rust code for interacting with the client.

Solana's Interface Definition Language (IDL) shares some similarities with Ethereum's Application Binary Interface Description Language (ADSL). Both are specifications for describing smart contract interfaces, including data structures and instructions.

<aside>
💡 While the `#[program]` macro encompasses various functionalities, its syntax is relatively straightforward. Let's build on this momentum and continue learning about the `Context` type. ✈️✈️✈️

</aside>

# Example

Here is a counter program implemented using the Anchor framework, which implements the initialization and accumulation functions of the counter.

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