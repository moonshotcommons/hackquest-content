# 8. Mantle - Initiating and Processing Transactions

# Content/Content

### Objectives

The goal of this section is to understand how a transaction is initiated and processed in the Mantle Network.

### **Initiating a Transaction**

- To initiate a transaction on the Mantle Network, Alice needs to ensure that she has a digital wallet like Metamask which is capable of interacting with the Mantle Network. The wallet should be configured with the RPC (Remote Procedure Call) node address of the Mantle network, enabling her wallet to send and receive information through the network.
    - About RPC: RPC stands for Remote Procedure Call, which is a communication mechanism that allows one computer (client) to request a specific task from a program running on another computer (server) through a network. In the context of blockchain technology, RPC acts as a bridge connecting users like Alice to the blockchain network like Mantle, enabling interaction between Alice's wallet device (client) and the nodes of the Mantle network (servers).
- When Alice wants to make a transaction on the Mantle blockchain:
    - She opens her digital wallet, selects the transfer function, and enters Bob's address and the amount she wants to transfer.
    - Before sending the transaction, the wallet checks if Alice's account balance is sufficient. If the balance is inadequate, the transaction cannot proceed.
        - How does the wallet know Alice's balance? There are typically two ways:
            - The wallet periodically calls the RPC interface to retrieve Alice's account balance from the Layer 2 network and caches it locally in the wallet.
            - A wallet provider's block crawler program retrieves real-time balance updates for Alice on the main chain and pushes the information to the wallet application.
    - Once the balance is confirmed to be sufficient, Alice clicks "Send." Her wallet software (client) sends a transaction request to a node in the Mantle network via RPC. This request includes the transaction details such as the recipient's address and the transfer amount.
    - Upon receiving Alice's transaction request, the Mantle node begins processing the transaction, marking the official start of the transfer process from Alice to Bob.

![Untitled](./img/8-1.png)

### **Processing Transactions**

- After Alice's transfer request is sent via the RPC node, a special node in the Mantle Network called the Sequencer receives and processes this request.
    - About the Sequencer: The primary task of the Sequencer is to efficiently sort and package received transactions (such as Alice's transfer request). The role of the Sequencer can be compared to a processing center in a postal system, where all received packages are sorted and packaged.
    - Mantle itself is built on the OP Rollup scaling solution, and the Sequencer is a common component in OP Rollup technology. It allows the Mantle network to process a higher volume of transactions, thereby improving transaction processing speed and reducing costs. In the Mantle architecture, the Sequencer collects, sorts, and packages transactions before submitting them to the main chain for final confirmation.
- The necessity of transaction packaging:
    - In Alice's transfer example, she is not the only one conducting transactions on the Mantle blockchain. At any given time, hundreds or thousands of users may be performing similar operations, such as transfers or executing smart contracts.
    - If the Mantle network were to immediately perform a rollup operation to the Layer1 network for each individual transaction, the processing time would significantly increase, potentially leading to network congestion.
    - Therefore, the Sequencer bundles multiple transactions, including Alice's and other users' transfer requests, into a block. This approach is similar to consolidating many small packages into a large package, thereby reducing the overall workload of rollups.
- Benefits brought by Sequencer:
    - Reducing Network Congestion: By accumulating multiple transactions before submitting them collectively, it significantly reduces the waiting time for new transactions on Layer 2, thus alleviating network congestion.
    - Improving Processing Speed: When transactions are merged and submitted as a block, the main chain only needs to verify and confirm that single block, instead of individually verifying and confirming hundreds or thousands of separate transactions. This greatly speeds up the overall processing speed.
    - Resource Efficiency: This approach reduces the computational and storage requirements on the main chain because processing a block containing multiple transactions is more resource-efficient than processing the same number of individual transactions.
- The Direct Impact of Mantle Compared to Ethereum on User Transactions:
    - For Alice, this means that her transfer requests on Mantle can be processed faster. Importantly, the transaction fees are much cheaper compared to transferring on the Ethereum mainnet. Through bundling, transaction fees are distributed among all the transactions in the block. Reducing transaction fees is particularly important for users who frequently engage in transactions and scenarios requiring large-scale transactions.

In conclusion, Sequencer in the Mantle Network not only improves the efficiency of transaction processing but also reduces the transaction costs for individual users through transaction bundling, making the entire blockchain network more economically efficient. For ordinary users like Alice, this method not only accelerates her transfer processing but also reduces her cost, thereby enhancing the practicality of blockchain technology.

![Untitled](./img/8-2.png)

### Next lesson

In the next lesson, we will learn how transactions are transmitted in the Mantle Network and ultimately submitted to a Layer 1 network.
