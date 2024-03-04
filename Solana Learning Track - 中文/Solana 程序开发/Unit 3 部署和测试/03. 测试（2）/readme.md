# Content

学习目标：优化测试脚本，对指定的数据账户进行累加。

通过上一节的学习，我们可以调用该 Solana 程序，并且得到累加后的预期值，但美中不足的是，每次调用都是创建一个新的账户，并且只能把它的值更新成1，那如何实现都某个数据账户一直累加呢？

这里我们不需要每次调用时创建一个新的数据账户，而是使用之前创建过的账户，这样才可以实现在某个账户上一直累加：

```jsx
import { PublicKey } from '@solana/web3.js';

const counterAccountPk = new PublicKey("3EsU9Tg8V186EEaPvfdYmrof996soBNBk8ivbsAxsM6w")
```

这里引入`PublicKey`依赖，并根据字符串格式的公钥，创建 Publickey 对象，***注意⚠️：这里的公钥为上节创建的密钥对`counterAccountPk`的公钥，我们在日志中有打印，可以记录下来并在此处填入，而非任意公钥。***

同时移除上一节的创建账户逻辑，只保留调用程序的指令逻辑，如下：

```jsx
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

构建程序调用的指令，并提交对应的交易，在链上完成计数器的累加，这样每次调用时，记得修改assert中的值，它跟我们的调用次数一致。

如上，就是 Solana 程序开发、编译、部署、测试的完整流程，通过这个简单的例子，相信你对 Solana 也有了更深的认识～

# Example/代码示例

以下为`native.test.ts`测试脚本完整内容，需要放在`Client→tests`文件夹下。

```jsx
// No imports needed: web3, borsh, pg and more are globally available
import { PublicKey } from '@solana/web3.js';

/**
 * CounterAccount 对象
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
 * CounterAccount 对象 schema 定义
 */
const CounterAccountSchema = new Map([
  [CounterAccount, { kind: "struct", fields: [["count", "u32"]] }],
]);

describe("Test", () = > {
  it("greet", async () = > {

    const counterAccountPk = new PublicKey("3EsU9Tg8V186EEaPvfdYmrof996soBNBk8ivbsAxsM6w")
    // 调用程序,计数器累加
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

    // 创建交易
    const tx = new web3.Transaction();
    tx.add(greetIx);

    // 发起交易，获取交易哈希
    const txHash = await web3.sendAndConfirmTransaction(pg.connection, tx, [
      pg.wallet.keypair,
    ]);
    console.log(`Use 'solana confirm -v ${txHash}' to see the logs`);

    // 获取指定数据账户的信息
    const counterAccountOnSolana = await pg.connection.getAccountInfo(
      counterAccountPk
    );

    // 反序列化
    const deserializedAccountData = borsh.deserialize(
      CounterAccountSchema,
      CounterAccount,
      counterAccountOnSolana.data
    );

    // 判断当前计数器是否累加
    assert.equal(deserializedAccountData.count, 4);
  });
});
```