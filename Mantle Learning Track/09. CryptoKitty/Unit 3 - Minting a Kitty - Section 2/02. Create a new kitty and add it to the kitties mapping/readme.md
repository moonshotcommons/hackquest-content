# Content/Create a new kitty and add it to the kitties mapping

In the previous step, we defined the ***_createKitty*** function. Now, we will create a new kitty by creating a new Kitty *struct* using the parameters.

First, Let's organize the *parameters* information: 

1. TokenId of the mother cat.
2. TokenId of the father cat.
3. generation.
4. Gene.
5. the owner of the Kitty.

However, we need one more attribute: ***birthTime***. In blockchain, the syntax block.timestamp is used to obtain the current block time.

Once we have all the information in the ***Kitty*** *struct*, we can create a kitty and then associate the TokenId of the NFT which will be minted in the next step with this kitty. Here comes ***_tokenIdCounter***.

**Syntax**

mapping

- hint
    
    ```solidity
    //For example, here we associate studentId with student information one by one.
    students[studentId] = Student(name,classId);
    ```
    
