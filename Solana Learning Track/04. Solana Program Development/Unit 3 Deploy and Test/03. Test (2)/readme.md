# Content

Learning Objective: Optimize the test script to increment a specified data account.

In the previous section, we learned how to call the Solana program and obtain the expected value after incrementing. However, a drawback is that each call creates a new account, and the value can only be updated to 1. ***How can we achieve continuous incrementation on a specific data account?***

Here, we don't need to create a new data account every time. Instead, we use a previously created account to achieve continuous incrementation:

```tsx
import { PublicKey } from '@solana/web3.js';

const counterAccountPk = new PublicKey("3EsU9Tg8V186EEaPvfdYmrof996soBNBk8ivbsAxsM6w");
```

We introduced the `PublicKey` dependency and created a `PublicKey` object based on the string format of the public key. ***Note⚠️: The public key here is the public key of the key pair `counterAccountPk` created in the previous section. It was printed in the logs and can be recorded and filled in here, rather than any random public key.***

At the same time, we removed the logic for creating an account from the previous section, keeping only the logic for calling the program's instruction, as shown below:

```tsx
const greetIx = new web3.TransactionInstruction({
  keys: [
    {
      pubkey: counterAccountPk,
      isSigner: false,
      isWritable: true,
    },
  ],
  programId: pg.PROGRAM_ID,
});
```

We build the instruction for calling the program and submit the corresponding transaction to complete the incrementation of the counter on the chain. Each time you make a call, remember to modify the value in the `assert` to match the number of calls.

This concludes the complete process of Solana program development, compilation, deployment, and testing. Through this simple example, we believe you now have a deeper understanding of Solana~

# Example

The following is the complete content of the `native.test.ts` test script, which needs to be placed in the `Client→tests` folder.

```jsx
// No imports needed: web3, borsh, pg and more are globally available
import { PublicKey } from '@solana/web3.js';

/**
  * CounterAccount object
  */
class CounterAccount {
   count = 0;
   constructor(fields: { count: number } | undefined = undefined) {
     if (fields) {
       this.count = fields.count;
     }
   }
}

/**
  * CounterAccount object schema definition
  */
const CounterAccountSchema = new Map([
   [CounterAccount, { kind: "struct", fields: [["count", "u32"]] }],
]);

describe("Test", () = > {
   it("greet", async () = > {

		 // Remember to replace this value with your own ！
     const counterAccountPk = new PublicKey("3EsU9Tg8V186EEaPvfdYmrof996soBNBk8ivbsAxsM6w")
     // Call the program and the counter accumulates
     const greetIx = new web3.TransactionInstruction({
       keys: [
         {
           pubkey: counterAccountPk,
           isSigner: false,
           isWritable: true,
         },
       ],
       programId: pg.PROGRAM_ID,
     });

     //Create transaction
     const tx = new web3.Transaction();
     tx.add(greetIx);

     //Initiate a transaction and obtain the transaction hash
     const txHash = await web3.sendAndConfirmTransaction(pg.connection, tx, [
       pg.wallet.keypair,
     ]);
     console.log(`Use 'solana confirm -v ${txHash}' to see the logs`);

     // Get the information of the specified data account
     const counterAccountOnSolana = await pg.connection.getAccountInfo(
       counterAccountPk
     );

     //Deserialize
     const deserializedAccountData = borsh.deserialize(
       CounterAccountSchema,
       CounterAccount,
       counterAccountOnSolana.data
     );

     // Determine whether the current counter is accumulating
     assert.equal(deserializedAccountData.count, 4);
   });
});
```