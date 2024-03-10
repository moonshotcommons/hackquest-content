# Content/Randomly generate genes

Previously, we mentioned that the ***createKittyGen0*** function needs to randomly generate the genes of a kitty, which is a `uint256` variable. Therefore, we need to use a random number generation algorithm.

In Solidity, a common approach to random number generation involves two built-in functions: ***keccak256*** and ***abi.encodePacked***.

> The ***keccak256*** function is a hashing algorithm that can convert a *string* value of any length into a *bytes32* hash value. Since different strings will always generate different hash values, we can use it to generate unique gene of each kitty if we have unique *string* value.
> 

We can use the ***abi.encodePacked*** function to encode distinct properties such as the current *timestamp* and TokenId to get a unique *string*, then apply the ***keccak256*** function to generate the hash. In this way, each **Gen-0 kitty** will have its own unique genes.

**Syntax**

keccak256

abi.encodePacked

- hint
    
    ```solidity
    //Here is an example of generating a random number based on a timestamp and a name.
    uint256(keccak256(abi.encodePacked(timestamp, name)))
    ```
    
