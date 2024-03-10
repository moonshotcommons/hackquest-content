# Content/Module

这是一节交互的内容！在这里你不会学习枯燥的代码，相反你需要回顾一下我们前几章学习的内容，我们会带你到在线 IDE - **Solana Playground** 当中去和该程序进行交互。

1. 打开 [Solana Playground](https://beta.solpg.io/) ，在左边的 **EXPLORER** 点击 **+** ，创建新的 Solana 项目：
    1. 输入项目标题
    2. 选择 Anchor(Rust)
2. 把我们前面的编写好的项目代码粘贴到 `src/lib.rs` 文件：
    
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
    
3. 把玩家的交互代码粘贴到 `client/client.ts` 文件：
    
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
    
4. 找到 Solana Playground 左边的工具栏，切换到第二个 **Build&Deploy** ，依次执行：
    1. **Build**
    2. **Deploy**
    
    至此，我们的程序就部署完成了。
    
5. 接下来，找到  `client/client.ts` 文件位置，点击 `Client` 的 **Run** 按钮，就可以初始化我们的程序并生成随机数；
6. 好了，我们已经生成好随机数了，找到`client/client.ts` 文件的倒数第二行`initialize();` ，这一行初始化代码就不需要了，我们给它加上注释 `//initialize();`；
7. 最后，就可以开始我们的猜数游戏了，在`client/client.ts` 文件找到最后一行 `guessing(0);`
    1. 取消注释；
    2. 修改 `guess` 函数参数，代表我们要猜测的数字；
    3. 并点击 `Client` 的 **Run** 按钮，就可以查看是否猜中。

恭喜你🎉，完成本课程！

# Content/Placeholder

[猜数.mov](./video/%E7%8C%9C%E6%95%B0.mov)