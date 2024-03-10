# Content/Module

This is an *interactive* lesson! Here, instead of learning dry code, you'll revisit the content we've covered in the previous chapters. We'll take you to the online IDE - **Solana Playground** to interact with the program.

1. Open [Solana Playground](https://beta.solpg.io/), click on *+* in the **EXPLORER** on the left to create a new Solana project:
    1. Enter the project title.
    2. Select Anchor(Rust).
2. Paste the code we wrote earlier into the ***src/lib.rs*** :
    
    ```rust
    use anchor_lang::prelude::*;
    use solana_program::clock::Clock;
    
    declare_id!("11111111111111111111111111111111");
    
    #[program]
    pub mod anchor_bac {
    		use super::*;
    		use std::cmp::Ordering;
    
    		pub fn initialize(ctx: Context<AccountContext>) -> Result<()> {
    				let guessing_account = &mut ctx.accounts.guessing_account;
    				guessing_account.number = generate_random_number();
    				Ok(())
    		}
    		
    		pub fn guess(ctx: Context<AccountContext>, number: u32) -> Result<()> {
            let guessing_account = &mut ctx.accounts.guessing_account;
            let target = guessing_account.number;
    
            match number.cmp(&target) {
                Ordering::Less => {
                    return err!(MyError::NumberTooSmall)
                }
                Ordering::Greater => {
                    return  err!(MyError::NumberTooLarge);
                }
                Ordering::Equal => {
                    return Ok(())
                }
            }
        }
    }
    
    fn generate_random_number() -> u32 {
    		let clock = Clock::get().expect("Failed to get clock");
    		let last_digit = (clock.unix_timestamp % 10) as u8;
    		let result = (last_digit + 1) as u32;
    		result
    }
    
    #[account]
    pub struct GuessingAccount {
    	pub number: u32,
    }
    
    #[derive(Accounts)]
    pub struct AccountContext<'info> {
    	
    	#[account(
            init_if_needed,
            space=32,
            payer=payer,
            seeds = [b"guessing pda"],
            bump
        )]
    	pub guessing_account: Account<'info, GuessingAccount>,
    
    	#[account(mut)]
      pub payer: Signer<'info>,
    	
    	pub system_program: Program<'info, System>,
    }
    
    #[error_code]
    pub enum MyError {
        #[msg("Too small")]
        NumberTooSmall,
        #[msg("Too larget")]
        NumberTooLarge
    }
    ```
    
3. Paste the player interaction code into the ***client/client.ts*** :
    
    ```rust
    const program = pg.program;
    const seeds = Buffer.from("guessing pda");
    const guessingPdaPubkey = anchor.web3.PublicKey.findProgramAddressSync(
      [seeds],
      program.programId
    );
    
    async function initialize() {
      try {
        const initializeTx = await program.methods
          .initialize()
          .accounts({
            guessingAccount: guessingPdaPubkey[0],
            payer: pg.wallet.publicKey,
            systemProgram: web3.SystemProgram.programId,
          })
          .rpc();
    
        console.log(
          "Initialize successfully!\n Your transaction signature is:",
          initializeTx
        );
      } catch (errors: any) {
        console.log(errors);
      }
    }
    
    async function guessing(number: number) {
      try {
        const guessingTx = await program.methods
          .guess(number)
          .accounts({
            guessingAccount: guessingPdaPubkey[0],
            payer: pg.wallet.publicKey,
            systemProgram: web3.SystemProgram.programId,
          })
          .rpc();
        console.log("Congratulation you're right!");
      } catch (errors: any) {
        console.log(errors.error.errorMessage);
      }
    }
    
    initialize();
    // guessing(0);
    ```
    
4. Find the toolbar on the left side of Solana Playground and switch to the second **Build&Deploy** tab, then sequentially execute:
    1. **Build**
    2. **Deploy**
    
    With this, our program is now deployed.
    
5. Next, locate the ***client/client.ts*** and click the **Run** button under `Client` to initialize our program and generate a random number;
6. Alright, now that the random number is generated, find the second-to-last line `initialize();` in the ***client/client.ts***. This line of initialization code is no longer needed, so let's comment it out with `//initialize();`;
7. Finally, we can start our guessing game. In the  ***client/client.ts***, find the last line `guessing(0);`
    1. Uncomment it;；
    2. Modify the ***guess*** function *parameter* to represent the number we want to guess;
    3. And click the **Run** button under `Client` to see if you guessed correctly.

🎉Congratulations, you have completed this course!

# Content/Placeholder

[猜数.mov](./video/猜数.mov)