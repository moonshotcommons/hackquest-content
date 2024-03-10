# Content

In this section we will discuss the differences between the two major blockchains - ***Solana*** and ***Ethereum***. Understanding their technical details and ecosystem differences is crucial for developers and ecosystem participants.

This section is an overall introduction to the content of Solana, and specific details will be expanded in the following chapters. We will introduce it from the aspects of consensus mechanism, transaction processing capabilities, transaction fees, smart contracts, accounts, programming languages and developer friendliness.

### **Section One: Consensus Mechanism**

**Solana** employs a combination of **`Proof of History (PoH)`** and **`Proof of Stake (PoS)`** to achieve transaction processing speeds of **thousands per second**. PoH, a unique and innovative mechanism, records and verifies timestamps and order of blocks. By introducing time proofs in each block, PoH allows nodes to quickly reach consensus without waiting for confirmation from the entire network. Solana's PoS mechanism is utilized for validator selection. Validators participate in network validation by staking a certain amount of tokens. Validators with more tokens have a higher chance of being chosen to generate new blocks and validate transactions. Thus, PoH ensures block timestamps and order, while PoS ensures network security and resistance to attacks, making Solana suitable for high-performance decentralized applications and high-frequency trading scenarios.

In September 2022, ***Ethereum*** completed the Ethereum 2.0 upgrade, transitioning from **`Proof of Work (PoW)`** to **`Proof of Stake (PoS)`**. This upgrade reduced the energy consumption required to secure Ethereum by **99.95%**, creating a more secure and environmentally friendly Ethereum network.

### **Section Two: Transaction Processing Capability**

**Solana** supports parallel processing of transactions by dividing them into subsets and assigning each subset to different validation nodes. This parallel processing significantly enhances transaction throughput while ensuring transaction security and reliability. Solana has an average block time of 400 milliseconds, processing over 2000 transactions per second on average, maintaining low transaction fees even during high loads.

***Ethereum*** processes transactions sequentially, with one transaction executed after another, updating the state sequentially. This limits Ethereum's throughput to an average of 15 to 30 transactions per second. However, Ethereum's transaction processing capability has been enhanced through the use of **`Layer2`** and the **`Rollup`** solution, bundling hundreds of transactions into a single transaction on the Ethereum network, reducing gas fees by up to 100 times. Additionally, the upcoming **Proto-Danksharding** upgrade in early 2024 is expected to further reduce gas fees and increase transaction throughput.

### **Section Three: Transaction Fees (Gas Fees)**

**Solana** calculates transaction fees dynamically based on the complexity and size of the transaction. This means that transaction fees vary according to the execution cost of the transaction, rather than the transaction volume on the network. Solana's average transaction fees are typically below $0.01, averaging around $0.00025, making it cost-effective for small transactions.

***Ethereum*** transaction fees fluctuate based on network congestion, a purely market-driven mechanism. In congested network conditions, users need to pay high fees for their transactions to be confirmed. Currently, the transaction fees for a simple transfer range from $1 to $10. However, the **`EIP-1559`** upgrade introduces a new fee market mechanism aimed at making fees more predictable.

### **Section Four: Smart Contracts**

In **Solana**, everything is an account, including smart contracts (referred to as **programs**). Programs are further divided into **executable accounts** (containing program code for specific logic execution) and **data accounts** (storing runtime data of the program). This separation simplifies program upgrades as the program itself is stateless and can be directly upgraded with new code logic.

***Ethereum*** smart contracts include both the logic code and state data. Once deployed, smart contracts do not support direct upgrades; only indirect upgrades are possible through redeployment, creating a new contract address, and proxying to the new contract address.

### **Section Five: Accounts**

In **Solana**, everything is an account, resembling a container (or a folder in a computer) that can hold program code, state data, and account metadata. Functionally categorized into **executable accounts** and **data accounts**, executable accounts store program code and are also known as program accounts. Data accounts include regular user accounts and other non-program accounts storing user balances, transaction history, and related data, without containing program code. While this account categorization might seem unusual for those familiar with Ethereum accounts, a deeper understanding reveals that Solana's single-account model enables parallel processing of multiple transactions, forming the foundation for Solana's high performance.

***Ethereum*** is divided into **EOA (Externally Owned Account)** and **Smart Contract** accounts. EOA are accounts for regular users in the Ethereum network, used to store Ether (ETH) and perform transactions. Smart Contract accounts include the logic code and state data of smart contracts created and deployed on the Ethereum blockchain. Through the combination of these two account types, Ethereum provides a flexible and powerful decentralized application development platform.

### **Section Six: Programming Language and Developer Friendliness**

**Solana** supports various programming languages, including **`Rust`** and **`C`**, known for their high performance.

***Ethereum*** uses the **`Solidity`** language designed for smart contract development, offering a plethora of development tools and a widespread developer community, providing abundant resources and support for newcomers.

### **Section Seven: Ecosystem and User Base**

**Solana** is rapidly establishing its ecosystem, though relatively newer compared to Ethereum, presenting numerous opportunities.

***Ethereum*** boasts the largest decentralized application (DApp) ecosystem and an extensive user and developer community, providing strong network effects and a higher degree of decentralization.

Through this comparison, it becomes evident that each platform has its own strengths and challenges. Ethereum's widespread adoption and mature ecosystem contribute to its stability and trust, while Solana's high performance and low costs offer advantages for applications requiring these features.