# Content/**Import the Standard Library for ERC721**

To use the ERC721 *standard*, we need to do three things:

1. import an ERC721 contract from the open library. 
2. initialize the *constructor* of the inherited *contract* when we define our *constructor.*
3. initialize the inherited *contract* constructor when defining our *constructor*.

Let’s do the first step. The widely recognized ERC721 *contract* is developed by OpenZeppelin, so let's import it into our *contract*.

**Syntax**

pragma, import

- hint
    
    ```solidity
    pragma solidity 0.8.17;
    import "ERC721.sol";
    ```
    
