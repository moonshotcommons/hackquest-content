# Content/完善**`AccountContext`的其他字段**

In this lesson, we will continue to complete the other fields in the ***AccountContext***. These fields provide references to the *payer account* and *the system program*, which are key components of the smart contract functionality.

1. **Adding the payer Field:** Represents the payer account required for executing the smart contract.
    
    ```rust
    #[derive(Accounts)]
    pub struct AccountContext<'info> {
        pub guessing_account: Account<'info, GuessingAccount>,
    
        #[account(mut)]
        pub payer: Signer<'info>,
    }
    ```
    
    - `#[account(mut)]`: Indicates that the ***payer*** is a *mutable* account reference, as the account state may be modified during contract execution (e.g., deducting fees).
    - `Signer<'info>`: ***payer*** is of *Signer* type, representing the entity conducting the transaction.
2. **添加 system_program 字段：**Represents a *reference* to the Solana system program, which provides some of the basic functionalities needed for contract execution.
    
    ```rust
    #[derive(Accounts)]
    pub struct AccountContext<'info> {
        pub guessing_account: Account<'info, GuessingAccount>,
    
        #[account(mut)]
        pub payer: Signer<'info>,
    
        pub system_program: Program<'info, System>,
    }
    ```
    

**Syntax**

struct

- hint
    
    ```rust
    #[derive(Accounts)]
    pub struct MyContext<'a> {
        pub my_account: Account<'a, MyAccount>,
        pub payer: Signer<'a>,
        pub system_program: Program<'a, System,
    }
    ```