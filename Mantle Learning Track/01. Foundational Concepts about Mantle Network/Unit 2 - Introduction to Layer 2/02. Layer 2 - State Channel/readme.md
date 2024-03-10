# 2. Layer 2 - State Channel

# Content/ Content

### Objective

The objective of this section is to learn about a Layer 2 implementation called state channels.

### Problem

Alice's company engages in cross-border transactions with other companies, and the individual transaction amount is relatively small, averaging around $100. Alice and her clients settle these transactions on the Bitcoin layer 1 network. Over time, Alice encountered the following issues:

1. To mitigate the risk of shipping goods without receiving payment, Alice and the other companies have to settle each transaction individually before proceeding to the next one (usually $100 per transaction). While it's manageable to bear the risk of a single transaction defaulting, the risk becomes unsustainable if both transactions are defaulted by the counterparty. Since each transaction typically takes about 10 minutes to settle on the Bitcoin layer 1 network, the daily transaction volume remains limited, preventing Alice from maximizing her earnings.
2. Due to the high transaction fees on the Bitcoin layer 1 network, Alice ends up earning less on each transaction. Consequently, she prefers higher-value orders to offset these fee losses.

### Solution

In light of these issues, Alice sought advice from Bob, who introduced her to a method called state channels. The specific solution is as follows:

- Every morning at 9 a.m., Alice and her client jointly create a multi-signature wallet (controlled by multiple private keys) and lock a certain amount of funds in this wallet. They record this transaction on the blockchain as evidence of opening the channel.
- Once the channel is established, Alice and her client can engage in frequent transactions within the channel. These transactions are not immediately submitted to the Bitcoin layer 1 network. Instead, both parties record the changes in transaction states locally and exchange updates with each other.
- Before the end of each workday at 6 p.m., when Alice and her client wish to close the channel, they can submit the final state to the Bitcoin layer 1 network. The Bitcoin network then verifies and executes this state update, which encompasses all the transaction information during the channel's operation.

As a result:

- Alice and her client can conduct an unlimited number of daily transactions within the channel. Transactions within the channel are fast, potentially allowing for 10 transactions per second, which is more than sufficient.
- Additionally, Alice only needs to pay the transaction fees on the Bitcoin layer 1 network once per day before closing the channel, saving her a significant amount of money.

However, since Alice and her client independently record transaction state changes locally, occasional inconsistencies may arise. In such cases, they need to establish a dispute resolution mechanism, as outlined below:

- If a dispute arises between Alice and her client, such as one party engaging in fraud or refusing to cooperate, they can choose to submit the dispute to the Bitcoin layer 1 network for resolution. During the dispute resolution phase, the Bitcoin layer 1 network verifies the dispute to determine the final state.
- One commonly used verification mechanism is Simplified Payment Verification (SPV).
- The key steps in the SPV verification process involve verifying the transaction's position and validity within the blockchain. Participants can use a Merkle tree structure to verify if a transaction is included in a specific block. A Merkle tree is a binary tree structure where each leaf node represents a transaction, and each non-leaf node's value is the hash of its child nodes' values. By comparing the transaction's hash with the Merkle tree's root hash, participants can confirm whether the transaction is included in the block.
- After layer 1 network verification and dispute resolution, the funds will be returned to their respective wallets according to the correct value.

With this solution, Alice's problems are resolved, and she is excited to try this approach the next day.

### Summary

In this section, we learned about state channels as a solution. The technical principles behind state channels are as follows:

1. Opening a channel: Participants lock a certain amount of on-chain assets in a multisignature contract to open a state channel.
2. Using the channel: Participants freely conduct transactions within the channel, updating the state locally without submitting to the blockchain.
3. Closing the channel: After unanimous agreement among all participants, the final state is submitted to the blockchain for the ultimate settlement. If no challenges are raised within a specified period, the transaction is considered completed.

State channels address the issues of delayed transaction settlement and high transaction fees.

### Next Lesson

We mentioned earlier that state channels resolve the issues of delayed transaction settlement and high transaction fees. However, are there any drawbacks to state channels? Take some time to think about it. In the next section, we will discuss the disadvantages of state channels and explore another implementation method for Layer2.

### Learn More

State channels are an off-chain scaling technique originally proposed by the Lightning Network in 2015. They enable participants to securely conduct off-chain transactions and settle the final outcome on the blockchain, minimizing interactions with the main network.

Some notable state channel projects:

- [Connext](https://connext.network/)
- [Kchannels](https://www.kchannels.io/)
- [Perun](https://perun.network/)
- [Raiden](https://raiden.network/)
- [Statechannels.org](https://statechannels.org/)

