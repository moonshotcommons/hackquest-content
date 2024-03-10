# 11. Mantle - Layer2 Data Storage

# Content/Content

### Objectives

The goal of this section is to learn about how Mantle Layer 2 data is stored.

### **EigenDA（Mantle DA）**

As Alice's transactions progress through various stages of processing and validation on the Mantle network, the validation signature data of the transactions is submitted by the Batch Submitter and recorded on the main chain's SCC. Now, our focus shifts to understanding where these original transaction data are stored and how their integrity and accessibility are ensured.

This introduces another crucial component of the Mantle Network - EigenDA (Mantle DA).

- Background:
    - In traditional blockchain, especially in Layer2 solutions like OP Rollups, although computations are offloaded to the off-chain layer, resulting in faster transaction speeds and reduced fees, the transaction data still needs to be packaged and published to Layer1. As the network participation rate continues to grow, the amount of data to be stored will significantly increase, posing a challenge to handle and store all transaction data. For example, although Alice's transfer is quickly processed on Layer2, the complete data still needs to be recorded and confirmed on Layer1 (such as the Ethereum mainnet).
    - Therefore, we require an efficient data storage solution that not only improves transaction throughput but also ensures the accessibility and verifiability of all transaction data. This is where EigenDA comes into play in the Mantle. As we learned earlier, SCC acts as a bridge between Layer2 and Layer1, storing compressed data proofs of the original transaction data. On Layer2, EigenDA stores the raw transaction data, seamlessly connecting transactions on the Mantle network across these two levels.
- Data Storage and Integrity Assurance
    - EigenDA serves as a data availability layer within the Mantle network and is responsible for storing all rollup transaction data. It functions as a vast digital archive, preserving the transaction records of Alice and other users.
    - Importantly, EigenDA not only stores data but also ensures its integrity and transparency, allowing anyone to verify the validity of transactions and blocks.
- Benefits
    - One of the key advantages of EigenDA is its ability to alleviate the burden on the main chain. By publishing only small compressed data to the main chain, it can process and store a larger volume of transaction data, thereby improving the overall system efficiency.
    - For users like Alice, this means experiencing faster transactions and lower costs directly.
- Other details
    - Currently, Mantle adopts the MantleDA solution supported by EigenLayer. Once EigenLayer's mainnet is launched, the more comprehensive EigenDA functionality can be directly utilized.

In summary, EigenDA plays a critical role as a data availability layer in the Mantle network. It ensures secure storage and fast access to all transaction data while greatly enhancing data processing efficiency and overall system performance through its advanced technology. For users like Alice, the presence of EigenDA makes their transaction experience smoother, secure, and transparent.

![Untitled](./img/11-1.png)

### Next lesson

With this, Alice's journey of transactions on the Mantle Network comes to an end. In the next section, we will review the interaction between Alice's transactions and Mantle to summarize the architecture of Mantle.
