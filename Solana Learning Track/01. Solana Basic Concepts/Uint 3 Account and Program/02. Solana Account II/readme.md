# Content

### Account Rent

In Solana's account model, there's a special concept called ***Rent***. Rent is distinct from transaction fees. Users pay rent to store data on the Solana blockchain, while transaction fees are paid for processing instructions on the network.

Unlike Ethereum, Solana charges an account on its network a fee for storing data state, which is the rent. If an account cannot afford the rent, the system deletes that account to reduce storage costs for data that is no longer maintained. An account can be exempted from paying rent if the assets in the account exceed the minimum balance for two years' rent. The rent storage cost on Solana is 0.00000348 SOL per byte, and a typical wallet data size is 372 bytes/year, requiring every active wallet holder to maintain 0.0026 SOL.

### **Types of Accounts**

- **User Account:** Regular wallet users, similar to Ethereum's External Owned Account (EOA).
- **Program Account:** Accounts that execute specific tasks, storing the program's binary file. We'll explore this further in upcoming sections.
- **PDA (Program Derived Addresses) :** These accounts store the program's state, i.e., data stored during program execution. It's a concept similar to Ethereum's state, but here, it's split into individual accounts. A dedicated section will cover this in the next part.
- **ATA (Associated Token Account) Accounts:** These are accounts associated with specific SPL (Solana Program Library) token, allowing users to conveniently manage the tokens they hold.

### **Definition of an Account**

Let's review the concept of Solana accounts through the definition of an account:

```rust
pub struct Account {
  /// Balance
  pub lamports: u64,
  pub data: Vec<u8>,
  pub owner: Pubkey,
  /// Whether it's an executable account
  pub executable: bool,
  /// Next epoch for rent collection
  pub rent_epoch: Epoch,
}
```

- ***lamports:*** Represents the account balance. Lamport is the basic currency unit in Solana, similar to Ethereum's **`wei`**.
- ***data:*** Represents the stored content, which is a byte array that can contain any type of data, such as program state, user asset information, and the bytecode of a stored program.
- ***owner:*** Indicates the public key of the program that owns or manages the account. It signifies which program has the right to operate on the account. If the account contains executable data, the **`owner`** represents the program that loads the account.
- ***executable:*** Indicates whether the account is executable. If **`true`**, it means the data in the account can be executed, making it a program account. If **`false`**, the account is used to store regular data, not executable code.
- ***rent_epoch:*** Represents the next period when rent will be deducted from the account. Solana uses the rent mechanism to prevent accounts from being indefinitely occupied without use, avoiding state bloat.
