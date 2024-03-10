# 7. Mantle - Modular Architecture

# Content/Content

### Objectives

The objective of this section is to learn about the modular architecture of the Mantle Network.

### **Modular Architecture**

When designing the Mantle Network, the Mantle team recognized the limitations of traditional Optimistic Rollup (OP Rollup) solutions. As a result, they introduced a modular Rollup design to improve efficiency and performance.
Modular architecture is an approach where the main functionalities of the blockchain, such as transaction execution, consensus, settlement, and data storage, are separated to different specialized layers. It's similar to how different departments in a large company have specific responsibilities for different aspects of the business.

![Untitled](./img/7-1.png)

What are the advantages of modular blockchain architecture?
Modular design allows for a more flexible and scalable system. Each layer can focus on its specific function and can be upgraded and optimized independently, minimizing the impact on other layers' functionalities. For example:

- Consensus Layer: Responsible for the consensus mechanism of the blockchain network, it can be optimized independently of transaction processing. We can introduce more efficient consensus algorithms to improve verification speed without affecting the efficiency of the execution layer and data layer.
- Data Layer: Handles data storage and transmission. For example, we can adopt new technologies to enhance scalability in the data layer, processing and storing larger volumes of transactions without compromising the security of the consensus mechanism and the computational speed of the execution layer.

This modular architecture enhances the overall performance of the blockchain system by allowing independent optimization of each layer, improving flexibility and scalability to meet future development needs.

### Next lesson

Alice heard that the Mantle Network has been designed and wants to experience it firsthand.
Starting from the next subsection, let's switch perspectives and imagine ourselves as Alice initiating a regular transaction through Mantle Network We'll explore how the system operates internally and the components involved in the entire lifecycle.
This way, we'll learn about the technical principles of Mantle from a first-person perspective. Exciting, isn't it?
