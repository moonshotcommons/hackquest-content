# 3. Layer 2 - Sidechains

# Content/ Content

### Objective

The objective of this section is to learn about one implementation of Layer 2, known as sidechains.

### Problem

1. Alice initially adopted state channels to facilitate transactions with her clients. However, Alice has a large number of clients spread across the globe, and managing individual state channels for each client has become challenging. Additionally, transactions within the state channels require both parties to sign, indicating their participation and agreement. Therefore, if Alice's company experiences a power outage or if she needs to take a break, the transactions can not proceed.
2. State channels only support simple transfer transactions, limiting Alice's ability to engage in activities such as discounts or upgrades.

### Solution

To address these issues, Alice sought advice from Bob, who introduced her to a solution called sidechains. The proposed solution is as follows:

- Alice and her clients collaborate to create a new blockchain called X. This blockchain operates with its independent consensus mechanism and rules, with participants including Alice, her clients, and reputable cross-border e-commerce companys.
- Alice and her clients lock a certain amount of BTC on the Bitcoin layer 1 network and generate an equivalent amount of BTC on the new sidechain X (SideBTC).
- On the sidechain, Alice can engage in various transactions and operations with her clients, including token transfers and smart contract executions.
- When Alice or her clients wish to transfer sidechain assets back to the Bitcoin layer 1 network, they lock the corresponding amount of sidechain assets and generate unlocking transactions on the Bitcoin layer 1 network. Once the unlocking transactions are confirmed, the corresponding amount of BTC is unlocked and becomes available on the Bitcoin layer 1 network.

With this solution, Alice's problems are resolved, and she is excited to try out this approach.

### Summary

In this section, we learned about sidechains as a solution. The technical principles of sidechains are as follows:

1. Sidechain Creation: Participants collaborate to create an independent blockchain called X, which has its consensus mechanism and rules.
2. Asset Locking: Participants lock a certain amount of BTC on the Bitcoin layer 1 network and generate an equivalent amount of SideBTC on sidechain X.
3. Sidechain Transactions: Participants can engage in various transactions and operations on sidechain X, including token transfers and smart contract executions.
4. Asset Transfer: When participants want to transfer sidechain assets back to the Bitcoin layer 1 network, they lock the corresponding amount of sidechain assets and generate unlocking transactions on the Bitcoin layer 1 network.
5. Asset Unlocking: After the unlocking transactions are confirmed on the Bitcoin layer 1 network, the corresponding amount of BTC is unlocked and becomes usable.

Sidechains address the challenges of managing a large number of state channels and the limitations of transaction types supported by state channels.

### Next Lesson

In the previous section, we discussed some of the problems that sidechains can address. However, are there any drawbacks to sidechains? Let's take a moment to consider this. In the next section, we will discuss the disadvantages of sidechains and explore another implementation of Layer 2.

### Learn More

Sidechains originated from the Bitcoin community and were proposed in December 2013. Blockstream led the development, and the technology was publicly announced in October 2014.

Sidechains are compatible blockchain networks that utilize cross-chain mechanisms to facilitate asset transfers from the main chain to the sidechain. They enable the deployment of applications on the sidechain, addressing congestion issues on the main chain. Compared to the main chain, sidechains are independent systems with further optimization potential in terms of technology and ideas, supporting more efficient consensus algorithms for transaction processing.

Representative projects:

- [Polygon PoS](https://polygon.technology/solutions/polygon-pos)
- [Skale](https://skale.network/)
- [Gnosis Chain (prev. xDai)](https://www.gnosischain.com/)
- [Loom Network](https://loomx.io/)
- [Metis Andromeda](https://www.metis.io/)