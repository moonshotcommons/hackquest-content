# Content

> In the previous chapters, we gained a preliminary understanding of Anchor. However, it seems that we haven't discovered the conveniences it brings to our program development. Now, let's delve deeper into the program structure of Anchor.
> 

After executing the `anchor init my_project` command, an Anchor sample project is automatically generated. The `lib.rs` file in this project is the core module of the Anchor framework, containing various macros. These macros generate Rust template code and corresponding safety checks for our program. The key macros used here are:

- **declare_id!**: Declares the **program address**. This macro creates a field to store the program address (`program_id`), allowing you to access a specific on-chain program with a specified `program_id`.
- **#[program]**: Holds the **business logic code** of the program. The implementation of the instruction functions will be done under the `#[program]` module.
- **#[derive(Accounts)]**: Due to the features of the Solana account model, most parameters are passed to the program in the form of an **account collection**. The structure decorated with this macro defines the collection of accounts that the program requires.
- **#[account]**: Decorates custom accounts needed by the program.

### Structure of the Anchor Framework

Taking the code on the right as an example, this program uses the `instruction_one` instruction function to receive data of type `u8` and store it in the on-chain `Counter` struct. In Solana, everything is an account, so the `Counter` struct is also a program derived account (PDA) for this program.

**1. Import Framework Dependencies:** Import the prelude module of the Anchor framework, which includes essential functionalities for writing Solana programs, such as `AnchorDeserialize` and `AnchorSerialize` (for deserialization and serialization), `Accounts` (macros for defining and managing program accounts), `Context` (provides information about the current program execution context, including accounts, system programs, etc.).

```rust
use anchor_lang::prelude::*;
```

**2. *declare_id! Macro*:** Specifies the Solana on-chain program address. When you first build an Anchor program, the framework automatically generates default key pairs for deploying the program. The corresponding public key becomes the program ID declared by the `declare_id!` macro.

In general, each time you build an Anchor Solana program, the program_id will be different. However, by specifying an address with the `declare_id!` macro, we can ensure that the address remains unchanged after program upgrades. This upgrade approach is much simpler compared to Ethereum's smart contract upgrades (using a proxy pattern).

```rust
// This is just an illustration; the actual program_id will be different
declare_id!("Fg6PaFpoGXkYsidMpWTK6W2BeZ7FEfcYkg476zPFsLnS");
```

**3. *#[program] Macro*:** Decorates the module containing all program instructions. This module implements the specific business logic for handling instructions. Each `pub`-decorated public function represents a separate instruction. The function parameters fall into two categories:

- The first parameter is of type `Context`, containing contextual information for processing the instruction.
- The second parameter is optional and represents the instruction's data.

**4. *#[derive(Accounts)] Program Derived Macro*:** Defines the list of accounts required for the instruction. This macro implements the serialization and deserialization Trait for the given `InstructionAccounts` struct. Consequently, there's no need for manual iteration over accounts or deserialization operations. It also implements safety checks to ensure that the accounts meet the requirements for secure program execution, with the `#[account]` macro complementing its usage.

**5. *#[account] Macro*:** Decorates custom accounts required by the program. It allows defining account attributes and implementing corresponding safety checks. Here, we've defined a counter `Counter`. Of course, more complex structures are possible, depending on the specific business logic.

<aside>
💡 In this section, we've gained an overall understanding of the Anchor framework. In the upcoming sections, we will delve into each macro individually.

</aside>

# Example

Here is a complete demo program implemented using Anchor.

```rust
//Introduce the pre-import module of the anchor framework
use anchor_lang::prelude::*;

//The on-chain address of the program
declare_id!("3Vg9yrVTKRjKL9QaBWsZq4w7UsePHAttuZDbrZK3G5pf");

//Instruction processing logic
#[program]
mod anchor_counter {
     use super::*;
     pub fn instruction_one(ctx: Context<InstructionAccounts>, instruction_data: u64) -> Result<()> {
         ctx.accounts.counter.data = instruction_data;
         Ok(())
     }
}

//The set of accounts involved in the instruction
#[derive(Accounts)]
pub struct InstructionAccounts<'info> {
     #[account(init, seeds = [b"my_seed", user.key.to_bytes().as_ref()], payer = user, space = 8 + 8)]
     pub counter: Account<'info, Counter>,
     #[account(mut)]
     pub user: Signer<'info>,
     pub system_program: Program<'info, System>,
}

// Custom account type
#[account]
pub struct Counter {
     data: u64
}
```