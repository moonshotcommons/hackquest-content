# Content/Define the burn function

Firstly, let's define the ***burn*** *function*. In this *function*, we aim to delete all the information of the **NFT** based on the TokenId. Therefore, we need an input *parameter* to represent TokenId.

Regarding the *function visibility*, although this *function* can delete the information of any NFT, we hope to provide this *function* as an interface to users.

> This is slightly different from the design of the ***deleteById*** *function*. The fundamental reason is whether we have the necessary to expose the *function* to users.
> 

To achieve this purpose, we can set this *function* as *public* and add some access control logic inside the *function*, such as only the owner of the NFT can **burn** it. We will discuss this in the following steps.

Now, let's define the *function*!

**Syntax**

function

scope

msg.sender

- hint
    
    ```solidity
    function brunApple(uint256 appleId) public {
    
    }
    ```
    
