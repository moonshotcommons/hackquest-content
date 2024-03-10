# Content

> In the previous section, we learned about the **`#[derive(Accounts)]`** macro, which provides validation for different ***account types*** in Anchor, including `Account`, `Signer`, `Program`, and more. You can find additional account types [here](https://docs.rs/anchor-lang/latest/anchor_lang/accounts/index.html).
> 

In this section, let's explore the ***account attribute constraints*** implemented by Anchor: **`#[account(..)]`**.

```rust
#[derive(Accounts)]
struct ExampleAccounts {
  #[account(
    seeds = [b"example_seed"],
    bump
  )]
  pub pda_account: Account<'info, AccountType>,

	#[account(mut)]
  pub user: Signer<'info>,
}
```

### **#[account(..)]** Macro Introduction

It is an attribute macro in the Anchor framework, offering a declarative way to specify account initialization, permissions, space (byte size), mutability, and other attributes. This simplifies interactions with Solana programs, acting as a form of account attribute constraint.

**1. Initialize a Program Derived Address (PDA):** The PDA is dynamically calculated based on `seeds`, `program_id`, and the automatically generated `bump` value (Anchor defaults to the first qualifying bump value). We don't need to manually specify the `bump`.

```rust
#[account(
	init,
	seeds = [b"my_seed"],
	bump,
	payer = user,
	space = 8 + 8
)]
pub pda_counter: Account<'info, Counter>,
pub user: Signer<'info>,
```

- ***init:*** Anchor initializes a program derived address (PDA) based on the specified attributes.
- ***seeds:*** Seeds are an arbitrary-length byte array, typically containing information required for the PDA address. In this example, we use the string `my_seed` as a seed. Other information, such as fields from the instruction accounts collection like `user` or parameters from the instruction function like `instruction_data`, can also be included:

```rust
#[derive(Accounts)]
#[instruction(instruction_data: String)]
pub struct InitializeAccounts<'info> {
		#[account(
			init,
			seeds = [b"my_seed",
							 user.key.to_bytes().as_ref(),
							 instruction_data.as_ref()
							]
			bump,
			payer = user,
			space = 8 + 8
		)]
		pub pda_counter: Account<'info, Counter>,
		pub user: Signer<'info>,
}
```

- ***payer:*** Specifies the paying account, i.e., the `user` account pays the transaction fee during account initialization.
- ***space:*** Specifies the account's space size as 16 bytes. The first 8 bytes store the discriminator automatically added by Anchor to identify the account type. The next 8 bytes allocate space for data within the `Counter` account type (`count` is of type u64, occupying 8 bytes).

**2. Validate a Program Derived Address (PDA):** Sometimes, when calling an instruction function, we need to verify if the provided PDA address is correct. We can use a similar approach by passing the corresponding `seeds` and `bump`. Anchor will calculate the PDA address based on these rules combined with `program_id` to perform the validation. Note: `init` attribute is not needed here.

```rust
#[derive(Accounts)]
#[instruction(instruction_data: String)]
pub struct InitializeAccounts<'info> {
		#[account(
			seeds = [b"my_seed",
							 user.key.to_bytes().as_ref(),
							 instruction_data.as_ref()
							]
			bump
		)]
		pub pda_counter: Account<'info, Counter>,
		pub user: Signer<'info>,
}
```

**3. `#[account(mut)]` Attribute Constraint:**

- ***mut:*** Indicates that this is a mutable account. In Solana programs, marking an account as mutable allows data (including balance) of this account to change during program execution.

The above are commonly used attribute constraints. Anchor provides many such attribute constraints, which can be found [***here***](https://docs.rs/anchor-lang/latest/anchor_lang/derive.Accounts.html)

<aside>
💡 In summary, **`#[account(..)]`** macro in Solana's Anchor framework is used for declaratively configuring account attributes. By specifying parameters in the macro, developers can indicate whether an account can be initialized, is mutable, requires a signature, define the payer, specify storage space size, and more. Importantly, through the `seeds` attribute, it conveniently generates program-derived address (PDA) by dynamically calculating the account address based on seed information combined with the program ID. This enhances code clarity and readability, helping developers adhere to Solana's account specifications and improving program maintainability and readability.

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
#[instruction(instruction_data: String)]
pub struct InitializeAccounts<'info> {
     #[account(
							init,
							seeds = [b"my_seed", user.key.to_bytes().as_ref(), instruction_data.as_ref()],
							payer = user,
							space = 8 + 8)
		 ]
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