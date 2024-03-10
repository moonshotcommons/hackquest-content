# 9. Mantle - Transmitting and Submitting Transactions

# Content/Content

### Objectives

The goal of this section is to understand how a transaction is transmitted and ultimately submitted to the mainnet.

### **Transaction Transmission**

- Once Alice's transaction is included in a block by a Sequencer, the block is ready for further processing and validation. However, other Mantle nodes are not aware of this transaction yet, so there needs to be an information transmission layer among Mantle network nodes to share the information about new transactions.
- This is where the Data Transport Layer (DTL) service comes into play. The DTL service is responsible for synchronizing the block data created by Sequencers. It acts as an efficient information distribution center, ensuring that every node in the network receives the latest block data.
- Synchronization with DTL:
    - Once a Sequencer completes the creation of a block, DTL retrieves the newly generated block data from the Sequencer.
    - It synchronizes the data not only with other regular nodes but also with other critical components in the network, such as nodes involved in transaction validation and confirmation (to be covered later).
    - This synchronization process is crucial for the overall functioning of the network, as it ensures that every participant in the network operates and validates based on the same up-to-date data.
- Direct impact on users:
    - For Alice, the efficient operation of DTL means that her transfer request is rapidly propagated and confirmed throughout the Mantle network.
    - This ensures that her transaction is not only processed quickly but also recognized and validated by other components in the network, thereby enhancing transaction reliability and security.

In summary, the Data Transport Layer (DTL) plays a crucial role in the Mantle network. It ensures timely synchronization of transaction data in the network and enables efficient and consistent network operation. For Alice and other users, this means that their transactions can be processed in a secure, reliable, and efficient environment.

![Untitled](./img/9-1.png)

### **Transaction Submission**

The component in Mantle responsible for submitting block transactions to a layer-one network is called the Batch Submitter.

Before introducing the Batch Submitter component, it's essential to understand the concept of StateRootData, as it is crucial for our upcoming discussions.

- In blockchain systems, especially in Layer 2 solutions, directly processing and storing all transaction data can be resource-intensive. This can result in slower processing speeds, increased storage requirements, and reduced overall network efficiency.
- To improve efficiency and reduce the burden on the main chain, it is beneficial to submit a compressed version of the entire data instead of all the data. This compressed version should be able to effectively verify the current state of blockchain. StateRootData, which we will discuss next, is one way to compress the entire data.
- In current Layer 2 solutions, one of the main goals is to alleviate the burden on the main chain. This is also true for Mantle. By submitting only partial proof data to the main chain, it is possible to reduce the resource requirements on the main chain while maintaining the security and immutability of Layer 2 transactions.

### **StateRootData**

- As mentioned above, processing and storing all transaction data in Layer 2 solutions can be resource-intensive. To improve efficiency and reduce the burden on the main chain, a more efficient method of data verification is needed. This is where the concept of StateRoot comes into play. It provides a compressed data representation that effectively represents the current state of the blockchain without the need to submit detailed information about all transactions.
- State Root is a cryptographic digest of the current complete state of the blockchain at a specific point in time. This includes account balances, smart contract states, and more.
- For example, when the state of the Mantle blockchain changes (e.g., when new transactions are included in a block), a new StateRoot is generated. This process typically involves complex cryptographic algorithms to ensure the uniqueness and accuracy of the StateRoot.

### **Batch Submitter**

With the prerequisite knowledge of StateRoot, when Alice makes a transaction to transfer funds to Bob on the Mantle blockchain, the transaction will be included in a block, and a new StateRoot representing the current state of the blockchain will be generated.

Now, the question arises: How does one use state root data? This is where the Batch Submitter comes into the picture.

- Responsibilities of the Batch Submitter:
    - The main task of the Batch Submitter is to collect the updated StateRoots resulting from the processing and inclusion of transactions by Sequencers into blocks.
    - Rather than directly submitting these StateRoot data to Layer 1, the Batch Submitter sends them to the Threshold Signature Scheme (TSS) module (to be discussed in detail later). The TSS module performs multiparty computation and signing to achieve preliminary verification before formal submission.
    - Nodes in the TSS module are responsible for validating the StateRoots' integrity and signing them. Once the StateRoots are confirmed to be valid, it signifies that the transactions included in the block are correct and trustworthy.
    - After confirming the validity of the StateRoots, the Batch Submitter submits the StateRoots to the layer-one network, such as Ethereum, for final inclusion and processing.
- The benefits of using the Batch Submitter:
    - By utilizing the Batch Submitter, Mantle can achieve efficient and secure transaction submission to the layer-one network.
    - The TSS module's preliminary verification ensures that only valid and trustworthy StateRoots are submitted to the layer-one network, enhancing the overall security and integrity of the Mantle blockchain.
    - The Batch Submitter also helps in reducing the burden on the layer-one network by submitting compressed StateRoot data instead of all the detailed transaction information.

In summary, the Batch Submitter component in the Mantle is responsible for collecting and submitting StateRoots, which represent the current state of the blockchain, to the layer-one network. It ensures efficient and secure transaction submission while reducing the burden on the layer-one network.

![Untitled](./img/9-2.png)

### Next lesson

In the next subsection, we will learn about how the TSS module performs preliminary transaction validation and how the SCC (State Commitment Chain) on Layer 1 processes the new blocks submitted by Mantle.
