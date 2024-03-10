# 12. Mantle - Architecture Overview

# Content/Content

### **Mantle Overview**

Alice's journey of transferring funds on the Mantle Network is now complete, showcasing the efficiency and security of the Mantle architecture. Her transactions are processed and packaged by Sequencers, and propagated through the Data Transfer Layer (DTL) in the network. The transaction states are verified using a Threshold Signature Scheme (TSS) and then submitted to the State Commitment Chain (SCC) smart contract to ensure records on Layer 1. At the same time, EigenDA stores the complete transaction data, ensuring data accessibility and verifiability. Finally, the Verifier Node acts as an additional security layer, ensuring data integrity and correctness throughout the network.

Alice's Mantle transfer journey demonstrates how Mantle ensures transaction security and transparency while maintaining transaction speed and reducing costs.

Below is a more detailed description of the interaction process to better understand the workings of each module:

1. Mantle Users: Users submit transactions through RPC nodes.
2. Sequencers: Upon receiving the transactions, Sequencers are responsible for packaging them into blocks. These blocks contain all the transaction data, including specific information such as addresses of the parties involved, transfer amounts, and data for smart contract calls.
3. Data Transfer Layer (DTL Service): This service synchronizes the block data created by Sequencers.
    1. Once Sequencers create the blocks, DTL retrieves the newly created block data from Sequencers and synchronizes it with other components in the Layer 2 network.
4. Verifier Node: The Verifier Node synchronizes Layer 2 block data from DTL and is responsible for checking the validity of the data.
    1. It verifies the Stateroot of each transaction block submitted by Sequencers to ensure that it matches the known correct state. This is done by comparing the data with Layer 1, ensuring the accuracy of the L2 data.
5. Batch Submitter: This component collects updated Stateroots and sends them to the Threshold Signature Scheme (TSS) module.
    1. Once the TSS nodes determine that the updated Stateroot is valid, the Batch Submitter publishes the signature data of the Stateroot to the SCC contract on L1.
6. Threshold Signature Scheme (TSS) Module: The nodes within this module verify the Stateroot provided by the Batch Submitter. If validated, they sign the rollup batches.
7. State Commitment Chain (SCC): SCC is a smart contract deployed on Layer 1 that receives the signed Stateroots from the Batch Submitter and records them on the Ethereum main chain.
    1. SCC can be understood as a bridge between Layer 2 and Layer 1, where anyone can verify whether the state updates on Layer 2 have been correctly recorded by checking the SCC contract on Layer 1.
    2. If there are any doubts about the data on Layer 2, the information on SCC can be used to verify and resolve disputes.
8. EigenDA (Mantle DA): This is where rollup transaction data is stored, ensuring data integrity and accessibility.
9. Verifiers and Fraud Proof: Verifiers can extract data from Mantle DA at any time to check its validity. If they discover any issues, Verifiers can challenge it by submitting Fraud Proof.
    1. Challenges: To address this challenge, the Layer 2 data (potentially disputed transactions and state updates) included in the Fraud Proof is published to the Layer 1 network.
    2. Verify: The smart contract on Layer 1 uses this data to perform state transitions, and if the state transition fails verification, it indicates that there are indeed errors in the Layer 2 updates. This mechanism provides a way to correct errors on Layer 2 and ensure the correctness of the entire network.

### **Summary**

By exploring Alice's fund transfer process on the Mantle Network, we not only gain an in-depth understanding of the efficiency and security of Mantle but also see how it ensures transaction security and transparency while maintaining transaction speed and reducing costs.

![Untitled](./img/12-1.png)

Thank you very much for participating in and completing this course on Mantle. We sincerely hope that this journey of deepening your understanding of Mantle has provided you with valuable knowledge of blockchain and has sparked your continuous interest in blockchain technology.

As a field that is constantly evolving and changing, blockchain is full of new challenges and opportunities. We hope you can maintain your curiosity, continue to explore, and look forward to meeting you again in future learning journeys!
