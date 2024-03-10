# Content/Define the mint function

After defining all *variables* and determining the issuer of the token. Now we can define the ***mint*** function!

Its purpose is to **mint** a specified amount of tokens to a target address. 

Therefore, we need two pieces of information here: how much are we **minting**, and who are we transferring the tokens to. These will be our *parameters*. 

We choose `uint256` for minting amount because it should not be negative and it might be a big number.

We will set the *function* to be `public`, because we expect the owner to call this *function* whenever they want. 

Here we don’t have any `return` because the user is not asking for any information here. 

**Syntax**

function parameters, function return, function calling,string, data location

- Hint
    
    ```solidity
    //For example, in this giveApple function, if we want to send apples to a specific address, we need to know their address and the amount to distribute.
    function distributeApple(address recipient, uint256 amount) public {
    
    }
    ```
    
