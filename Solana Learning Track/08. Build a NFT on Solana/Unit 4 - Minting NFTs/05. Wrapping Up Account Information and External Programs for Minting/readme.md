# Content/**Implementing the Creation of `cpi_ctx`**

In this lesson, we'll learn how to create ***cpi_ctx*** within the ***mint_nft*** function. 🌍 ***cpi_ctx*** is of type `CpiContext`, provided by the Anchor framework. It encapsulates all the necessary information for Cross-Program Invocation (CPI), including the program to call and the relevant accounts.

**Creating *cpi_ctx*:**

In the last two lessons, we've defined ***cpi_program*** and ***cpi_accounts***, which represent the program to call and the related accounts for token minting. Now, let's use these variables to build our ***cpi_ctx***:

```rust
pub fn mint_nft(
        ctx: Context<MintNFT>,
        creator_key: Pubkey,
        uri: String,
        title: String) -> Result<()> {
        
		let cpi_accounts = MintTo {
	      mint: ctx.accounts.mint.to_account_info(),
        to: ctx.accounts.token_account.to_account_info(),
        authority: ctx.accounts.payer.to_account_info(),
    };

		let cpi_program = ctx.accounts.token_program.to_account_info();
		let cpi_ctx = CpiContext::new(cpi_program, cpi_accounts);
}
```

`CpiContext::new`: This function creates a new `CpiContext` instance. It takes two arguments: ***cpi_program*** (the account information of the program to call) and ***cpi_accounts*** (the collection of accounts involved in CPI).

Starting from the next lesson, we'll use ***cpi_ctx*** to execute cross-program invocations and create our NFTs.

**Syntax** 

function

- hint
    
    ```rust
    pub fn my_function(ctx: Context<MyContext>) -> Result<()> {
        let cpi_ctx = CpiContext::new(my_program, my_accounts);.
    }
    ```