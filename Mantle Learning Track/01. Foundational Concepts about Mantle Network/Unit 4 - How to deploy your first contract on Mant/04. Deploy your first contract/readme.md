# Deploy your first contract

# Content/Deploy

Sure! Currently, our wallet has a certain **MNT**, and we can try using these tokens to perform some simple operations, such as deploying a smart contract on the Mantle.

Usually, there are several basic steps for contract deployment:

- Write a simple *smart contract*
    
    > For demonstration, we provide a simple ***HelloWorld** contract* here.
    > 
- Test the contract
- Click Try it out button to open HackQuest IDE
- Deploy on Remix VM
    1. Compile the *contract*.
        
        ![Untitled](./img/4-1.png)
        
    2. Use Remix VM to deploy the contract, here we choose Remix VM (Shanghai)**.**
        
        ![Untitled](./img/4-2.png)
        
    3. Test ***get***.
        
        ![Untitled](./img/4-3.png)
        
    4. Test ***set***.
        
        ![Untitled](./img/4-4.png)
        
        ![Untitled](./img/4-5.png)
        
- Deploy contract on BlockChain
- Deploy on Mantle
    1. Compile the *contract*.
        
        ![Untitled](./img/4-6.png)
        
    2. Choose Injected Provider - MetaMask to connect the wallet.
        
        ![Untitled](./img/4-7.png)
        
    3. Click “**Deploy**” and confirm the transaction.
        
        ![Untitled](./img/4-8.png)
        
- Verify the deployment of the contract.
- Query Contract in Blockchain Explorer.
    
    Congratulations! With the successful deployment, we now have a contract that is truly on the blockchain. It will permanently run on the **blockchain**, and we can view the corresponding *contract* information using the contract address in [the blockchain explorer provided by Mantle](https://explorer.testnet.mantle.xyz/)!
    
    ![Untitled](./img/4-9.png)
    
    ![Untitled](./img/4-10.png)
    
    ![Untitled](./img/4-11.png)
    

# Example/Code

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.17;

contract HelloWorld {
    string public greeting;

    constructor() {
        greeting = "Hello, HackQuest!";
    }

    function getGreeting() public view returns (string memory) {
        return greeting;
    }

    function setGreeting(string memory _newGreeting) public {
        greeting = _newGreeting;
    }
}
```