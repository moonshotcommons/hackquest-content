# 5. Layer 2 - ZK Rollup

# Content/ Content

### Objective

The goal of this section is to learn about a Layer 2 implementation called ZK Rollup.

### Problem

1. Alice started using Optimistic Rollup for transactions with her clients, where a challenge mechanism exists to prevent Alice from cheating, as cheating would result in punishment.
2. However, among Alice's clients, there is a wealthy individual who was unsuccessful in pursuing Alice. Out of frustration, he decided to launch relentless attacks on Alice's system. Every day, he would challenge the transactions submitted by Alice. Although Alice did not cheat, he would not be affected by the monetary penalties for unsuccessful challenges due to his wealth. Each challenge would cause delays, and the main chain would remain in a prolonged dispute resolution period. Alice's clients became hesitant to conduct transactions because of frequent disputes, and they felt uneasy.
3. On the other hand, whenever Alice's clients wanted to withdraw funds from Layer2 to the main chain, they had to wait for the entire challenge period, typically seven days. They found the efficiency of fund transfers to be unsatisfactory. They expressed their concerns to Alice multiple times.

### Solution

Due to these issues, Alice sought advice from Bob, who introduced her to a method called Zero-knowledge (ZK) Rollup. The specific solution is as follows:

- Alice informed her clients that they would no longer have a challenge period and that they would mathematically prove the validity and integrity of the transactions she submitted to the main chain.
- However, other clients asked why they should trust her. Alice explained that there is a mathematical method that allows her to submit only a commitment without revealing all the transaction details. Through this commitment, they can verify that she did not cheat.
- Seeing the puzzled expressions on her clients' faces, Alice used an analogy:
    - Suppose I am a mathematician, and I know a formula, but I don't want to disclose the formula. However, I want to prove that I know the formula.
    - As long as you give me an input, I can provide you with an output within a limited time. You have the ability to verify that the output is correct. If you ask me ten thousand times and I'm correct every time, based on mathematical probability, I most likely know the formula. So, you can trust me.
    - This is the principle of zero-knowledge proof. If you don't believe me, you can ask Bob or consult scholars in the academic community.
- The clients consulted some professors and discovered that this concept actually exists. They agreed and decided to start using this method.
- Alice and her clients invested some money to outsource the implementation of this solution. One month later, they happily began using the new system called ZK Rollup. Each transaction submission no longer required a challenge because it was mathematically proven to be tamper-proof.

With this solution, Alice's problems were resolved, and she was very pleased, intending to continue using this approach.

### Summary

In this section, we learned about ZK Rollup as a solution. Its technical principles are as follows:

1. Construct a sidechain: Create an independent sidechain, typically based on the Ethereum Virtual Machine (EVM) or a compatible chain. This sidechain can be a standalone blockchain or a rollup partition.
2. Execution and batch submission: Execute smart contract transactions on the sidechain and batch submit these transactions according to certain rules. Each batch typically contains multiple transactions.
3. State transition and merging: Upon each batch submission, record the state transition on the sidechain and merge it with the previous state. This gradually updates and accumulates the sidechain's state, reflecting the state transitions of all submitted batches.
4. Zero-knowledge proofs: During each batch submission, to ensure the correctness and verifiability of state transitions on the sidechain, use zero-knowledge proofs to prove that the execution of each batch's transactions is correct without revealing detailed transaction contents. This protects the privacy of transactions.
5. Main chain submission: Regularly (typically per batch or at certain time intervals), submit the sidechain's state root hash and the corresponding zero-knowledge proof to the Ethereum main chain. This submission acts as a digest and proves the validity of state transitions on the sidechain, allowing verification on the main chain.
6. Main chain verification: On the Ethereum main chain, validators can verify the submitted state root hash and zero-knowledge proof to ensure the correctness of state transitions on the sidechain. Validators can perform verifications as needed and have the opportunity to participate in the consensus mechanism on the main chain.

ZK Rollup addresses the ongoing disputes in Optimistic Rollup and the lengthy challenge period necessary for security reasons.

### Next Lesson

We mentioned some of the problems that ZK Rollup can solve.
But does ZK Rollup itself have any drawbacks? Students can contemplate this question.
In the next lesson, we will discuss the drawbacks of ZK Rollup and begin learning about the Mantle public chain.

### Learn More

The origin of ZK Rollup can be traced back to the Israeli company StarkWare, founded in 2018 by Israeli engineers Eli Ben-Sasson and Alessandro Chiesa, among others. ZK Rollup utilizes zero-knowledge proofs to prove the validity of transactions without revealing specific transaction information. This approach emphasizes privacy, security, and independence from main chain verification.
Representative projects:

- [zkSync](https://zksync.io/)
- [ZKSpace](https://zks.org/)
