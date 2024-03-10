# 4. Layer 2 - OP Rollup

# Content/ Content

### Objective

The goal of this section is to learn about a Layer2 implementation called Optimistic (OP) Rollup.

### Problem

1. Alice initially used sidechains for conducting transactions with her clients. However, the node operators on these sidechains were Alice's clients and some well-known cross-border companys. Due to Alice's company's excessive profits and strong brand reputation, her competitors became jealous. They conspired with Alice's clients to manipulate the node operations and transfer all of Alice's funds. Since sidechains have independent consensus mechanisms and rules, an attack can be launched if a certain proportion of malicious nodes is reached.
2. Alice became aware of this plot because one of her clients happened to be a close friend of her aunt. Alice had to address this issue promptly; otherwise, her business would suffer, and she could even lose her capital.

### Solution

To address these problems, Alice sought advice from Bob, who introduced her to a method called Optimistic Rollup. The specific solution is as follows:

- Alice informed her clients that they would no longer serve as nodes due to the risk of collusion. She would assume the role of the sole node operator and batch compress all transactions onto the Bitcoin layer 1 network.
- However, the other clients expressed concerns about transferring the risk onto themselves. They strongly opposed this approach.
- Eventually, Alice and her clients devised a solution by creating a challenge mechanism. This mechanism would allow anyone to challenge the final transaction state submitted to the layer 1 network. The layer 1 network would perform verification, and if any malfeasance by Alice were detected, the system would punish her by redistributing her funds to everyone else.
- Implementing such a challenge mechanism on the original Bitcoin layer 1 network proved challenging due to Bitcoin's limited programmability. However, they discovered a new Layer 1 called Ethereum, which natively supports smart contracts and allows for the implementation of complex business logic. Alice consulted Bob again to confirm the technical feasibility of this method.
- Alice and her clients allocated resources to outsource the development of this solution. After one month, they happily started using the new system called Optimistic Rollup.

With this solution, Alice's problems were resolved, and she was delighted to continue using this approach.

### Summary

In this section, we learned about Optimistic Rollup as a solution. Its technical principles are as follows:

1. Sidechain construction: Create an independent sidechain, typically based on the Ethereum Virtual Machine (EVM) or a compatible chain. This sidechain can be a standalone blockchain or a rollup.
2. Execution and verification: Execute smart contract transactions on the sidechain and verify their results. Verification is typically performed by running validation nodes on the sidechain.
3. State submission: After executing and verifying transactions on the sidechain, only the submission information of the state needs to be sent to the Ethereum main chain. This submission information usually includes the state root hash from the sidechain and some proof data to demonstrate the correctness of the computation on the sidechain.
4. Dispute resolution: Once the state is submitted to the Ethereum main chain, a dispute resolution period begins. During this period, anyone can raise disputes against the submitted state and provide relevant evidence. Dispute resolution mechanisms are typically based on optional arbitrators or community voting to determine the validity of the submission.
5. Rollback and rewards: If no disputes or resolved disputes are confirmed as invalid, state transitions on the sidechain are considered valid. In such cases, transactions on the sidechain are approved, and participants receive corresponding rewards. If a dispute is resolved and confirmed as valid, the state transition on the sidechain is rolled back, potentially leading to penalties for the involved participants.

Optimistic Rollup addresses the issue of sidechains being vulnerable to collusion among nodes.

### Next Lesson

We mentioned some problems that Optimistic Rollup can solve. But does Optimistic Rollup itself have any drawbacks? Let's consider this question in the next section. Afterward, we will learn about another implementation approach for Layer 2.

### Learn More

The concept of Optimistic Rollup was first proposed by Joseph Poon in 2018. This approach is based on an "optimistic" assumption that transactions submitted on the main chain are presumed valid unless disputes arise. The design philosophy aims to improve transaction throughput and reduce the burden on the main chain. Mantle Network adopts this approach in its implementation.

Representative projects:

- [Mantle Network](https://www.mantle.xyz/)
