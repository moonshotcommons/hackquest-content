# Content

### **Roles in Solana's Architecture: Leader and Validator**

In Solana's system architecture, two crucial roles are **Leader** (block producer) and **Validator**. Both are full nodes staking SOL tokens, but they alternate between different nodes as Leaders during block-producing cycles. Nodes that are not elected as Leaders become Validators. Solana employs a ***Proof of Stake*** (PoS) mechanism in choosing Validators, where stakers participate in network transaction verification by staking a certain amount of tokens. Validators with more tokens staked have a higher chance of being selected to generate new blocks.

![Untitled.png](./img/1-1.png)

1. After a user initiates a transaction, it is either directly forwarded to the Leader node by the client or initially received by regular nodes and then promptly forwarded to the Leader.
2. The Leader receives all pending transactions within the network, executes them, orders transaction instructions, and creates a transaction sequence (similar to a block). At regular intervals, the Leader sends the sorted transaction sequence to Validators.
3. Validators execute transactions in the given order from the transaction sequence (block), producing corresponding state information (executing transactions changes the node's state, such as altering balances of certain accounts).
4. After sending N transaction sequences, the Leader periodically publishes the local state. Validators compare it with their own state and provide affirmative or negative votes. This step is akin to "checkpoints" in Ethereum 2.0 or other PoS blockchains.
5. If, within the specified time, the Leader collects affirmations from nodes with 2/3 of the total staking weight in the network, the previously released transaction sequence and state are finalized. This is equivalent to achieving final confirmation (Finality) for the block.
6. Generally, Validators that give affirmative votes have the same executed transactions and resulting state as the Leader. Data is synchronized.

### **Selecting Leaders in Solana**

In Solana's consensus protocol, there are two significant time units: ***Epochs*** and ***Slots***. Each Slot is approximately 0.4 to 0.8 seconds, equivalent to the time interval of one block. Each Epoch cycle consists of 432,000 Slots, lasting 2 to 4 days. Every 4 Slots (block-producing cycle), Leader nodes undergo a change.

![Untitled.png](./img/1-2.png)

At the beginning of each new Epoch cycle, the Solana network selects Leaders based on the staking weights of each node, forming a rotation list of block producers, "designating" the future block producers at different times. In other words, block producers are informed in advance that they will be block producers. Factors considered in Leader selection include:

1. **Amount of staked tokens:** The quantity of staked tokens is a crucial consideration in PoS. Validators typically prefer nodes with larger staked amounts, increasing the chances of a node being selected as a block producer. This also helps ensure that the network is maintained by nodes with sufficient vested interest.
2. **Node performance:** Node performance is another key factor. High-performance nodes can verify and package transactions more quickly, contributing to maintaining a high throughput network. Validators may choose nodes with better performance to enhance overall network efficiency.
3. **Network latency:** Validators may consider network latency between nodes. Opting for nodes with lower network latency helps reduce block propagation time, enhancing network real-time performance.
4. **Node availability:** Validators focus on node availability, ensuring stable operation without easy susceptibility to faults. Reliable nodes can provide more stable services to the network.

The goal of Leaders is to select a suitable set of transactions, ensuring network security, efficiency, and fairness. By comprehensively considering these factors, Solana can make optimal block-producing decisions, driving the network's normal operation.

### **Recap**

Now, after understanding the fundamental details, let's take a look at how Solana's network operates through PoH and PoS:

1. **Transaction Generation:** Users create and broadcast transactions, including detailed transaction information and digital signatures.
2. **Ordering on PoH Chain:** Transaction hashes are linked to the PoH chain via digital signatures. As the PoH chain is ordered, transactions are also sorted.
3. **Validation by Validators:** Validators are responsible for validating the transactions' validity and choosing which transactions will be included in the next block. This selection may be based on factors like the quantity of staked tokens, Validator performance, and more.
4. **Transaction Packing into Blocks:** The transactions chosen by Validators are packaged into a block, including a special block-producing transaction containing the current PoH chain's hash and other information.
5. **Block Propagation and Confirmation:** The block is broadcasted to the entire network. Other nodes verify and confirm the block's validity. Once confirmed, the block and its contained transactions are added to the entire blockchain.

Through this process, Solana achieves the circulation of transactions and the update of the entire blockchain through the ordered time of the PoH chain and the node verification mechanism of PoS. This design compresses Solana's average block time to 400 milliseconds, attains high speed without the need for Layer 2, and incurs negligible transaction fees.