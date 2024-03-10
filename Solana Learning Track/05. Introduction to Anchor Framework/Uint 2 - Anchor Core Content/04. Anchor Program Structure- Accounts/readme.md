# Content

In the previous section, we learned that using `ctx.accounts` allows us to access the account collection `InitializeAccounts` of the instruction function. It is a struct that implements the `#[derive(Accounts)]` derived macro. This macro generates handling logic related to Solana program accounts for the struct, making it easier for developers to access and manage these accounts.

```rust
// anchor_lang::context
pub struct Context<'a, 'b, 'c, 'info, T> {
    pub accounts: &'b mut T,
    // ...
}

#[program]
mod anchor_counter {
    pub fn initialize(ctx: Context<InitializeAccounts>, instruction_data: u64) -> Result<()> {
        ctx.accounts.counter.count = instruction_data;
        Ok(())
    }
}

#[derive(Accounts)]
pub struct InitializeAccounts<'info> {
    #[account(init, payer = user, space = 8 + 8)]
    pub counter: Account<'info, Counter>,
    // ...
}
```

### #[derive(Accounts)] Macro

This macro is applied to the list of accounts required by the instruction, implementing deserialization functionality for the given struct data. ***Therefore, manual iteration of accounts and deserialization operations are no longer necessary when retrieving accounts. It also implements security checks required for the safe execution of the program. Of course, this requires the use of the `#[account]` macro.***

1. Let's look at the `InitializeAccounts` struct in the example. When the `initialize` instruction function is called, the program performs the following two checks:

```rust
#[derive(Accounts)]
pub struct InitializeAccounts<'info> {
    #[account(init, seeds = [b"my_seed", user.key.to_bytes().as_ref()], payer = user, space = 8 + 8)]
    pub pda_counter: Account<'info, Counter>,
    #[account(mut)]
    pub user: Signer<'info>,
    pub system_program: Program<'info, System>,
}
```

- **Account Type Verification:** Checks whether the passed accounts match the account types defined in `InitializeAccounts`, such as `Account`, `Signer`, `Program`, and other types.
- **Account Permission Verification:** Based on the permissions annotated on the accounts, the framework performs corresponding permission checks, such as checking for sufficient signing authority or whether modification is allowed.

If any of these checks fail, it results in a failed instruction execution and generates an error.

1. The `InitializeAccounts` struct has three types of accounts:

 2.1. `Account` Type: It is a wrapper around the `AccountInfo` type and is used to verify account ownership and deserialize underlying data into Rust types. For the `counter` account in the struct, Anchor implements the following functionalities:

```rust
pub pda_counter: Account<'info, Counter>,
```

① Automatic deserialization of data for this account type Counter.

② Checking whether the passed owner matches the owner of Counter.

 2.2. `Signer` Type: This type checks whether the given account has signed the transaction but does not check ownership. Signer type should only be used when underlying data is not needed.

```rust
pub user: Signer<'info>,
```

 2.3. `Program` Type: It verifies that this account is a specific program. For the `system_program` field, the Program type is used to specify that the program should be a system program, and Anchor performs the validation for us.

```rust
pub system_program: Program<'info, System>,
```

Here, we've only introduced the account types in `#[derive(Accounts)]`. In fact, each field also has the `#[account(..)]` attribute macro, which we will cover in the next section.

<aside>
💡 In summary, **`#[derive(Accounts)]`** is a macro in the Anchor framework that simplifies account handling code in Solana programs. By annotating struct properties, it automatically generates account operation logic, improving readability and maintainability, allowing developers to focus more on business logic.

</aside>

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
     pub pda_counter: Account<'info, Counter>,
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