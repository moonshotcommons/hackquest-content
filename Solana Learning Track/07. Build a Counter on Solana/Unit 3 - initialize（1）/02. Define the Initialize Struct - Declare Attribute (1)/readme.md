# Content/Attribute Declaration

In the previous lesson, we defined the framework of the ***Initialize*** struct. Now, we need to specifically fill in this *struct*.

- Do you remember the two prerequisites we discussed in the last lesson?
    - Where will the counter's data be stored?
    - Who has the authority to initialize this counter?

Now, let's address the first question by adding an attribute to the initialization struct.

**Counter Account - counter**:

- This attribute is used to store *count data* and is the core of the entire initialization process.

To ensure that this account is correctly initialized and meets our requirements, we can use `#[account(…)]` to add a series of specific attribute configurations to it:

- We need to create a new account
    
    If the ***counter*** account does not exist before the program execution, we need to create it, as we require a *dedicated account* to securely store the ***counter's*** data.
    
- We need to specify who pays the fee for creating the counter account
    
    On Solana, creating a new account *consumes resources*, so an existing account needs to pay these fees.
    
- We need to pre-allocate space for this account
    
    On Solana, the storage space for accounts is limited and needs to be *allocated in advance* when creating the account. Therefore, we need to explicitly specify the size of the storage space required for the ***counter*** account.
    
- We need to generate an address
    
    On Solana, each account has a unique address for identification and access. For the ***counter*** account, we use a *Program Derived Address (PDA)* to ensure its uniqueness and security. A PDA is a special type of address that is associated with an on-chain program and can provide additional security and functionality.
    

**Syntax**

#[account(…)]，Struct

- hint
    
    ```rust
    #[derive(Accounts)]
    pub struct Initialize<'info> {
        #[account(
            init,
            payer = authority,
            space = Counter::SIZE,
            seeds = [b"counter"],
            bump
        )]
        counter: Account<'info, Counter>,
    }
    ```