# Content/Define the transfer function

In this section, we will define a function called ***transfer***.

To complete a **transfer**, we need to know:

- Sender
- Recipient
- Transfer amount

In theory, we need three *parameters*, but since the *function* caller can be considered as the sender, we can obtain it using the `msg.sender` syntax.

Therefore, in the ***transfer*** *function*, we only need two *parameters*, named ***recipient*** and ***amount.*** Among them, the ***recipient*** is an `address`; the ***amount*** is a *non-negative number*, thus we choose unsigned integer `uint256` to represent it.

We choose `public` as the *function*'s visibility because the *function* serves as a public interface that can be called by anyone.

`Return` a value of type `bool` to indicate whether the **transfer** was successful.

**Syntax**

function,scope

- hint
    
    ```solidity
    //For example, this transferApples function can be used to transfer apples between users
    function transferApples(address recipient, uint256 amount) public returns(bool){
    
    }
    ```
    
