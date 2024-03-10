# Content/Content

### Concept

In the previous article, we learned about *string*. In this tutorial, we’re going to focus on string concatenation.

*String concatenation* is the process of combining two or more *strings* into a single *string*. 

![string_concat.png](./img/3-1.jpeg)

- Metaphor
    
    Think of a string in Solidity as a string of beads. Each bead represents a character. Just as you can add new beads to the string, remove existing ones, or rearrange them, a *string* in Solidity allows you to change its content and length even after it has some initial characters.
    
    Concatenation of strings is like joining two or more strings of beads end-to-end. Each string has its own set of beads (characters), and when you concatenate them, you're creating a longer string of beads that combines the characters from all the original strings. This can be very useful when you need to create a new string that includes parts of existing strings.
    
- Real Use Case
    
    In the ERC721 standard for NFTs, each NFT is uniquely identified by a token ID. The ***[tokenURI](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9e3f4d60c581010c4a3979480e07cc7752f124cc/contracts/token/ERC721/ERC721.sol#L96)*** function in the ERC721 standard is used to create a unique URI for each NFT by joining together two strings: a base URI  and the token ID.
    
    The base URI is common to all NFTs in the contract, while the token ID is unique for each NFT. By joining these two strings together, the ***[tokenURI](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9e3f4d60c581010c4a3979480e07cc7752f124cc/contracts/token/ERC721/ERC721.sol#L96)*** function creates a unique URI for each NFT. This URI is used to access information about the NFT, such as its name, image, or other details.
    
    Below is the code implementation of the ***[tokenURI](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9e3f4d60c581010c4a3979480e07cc7752f124cc/contracts/token/ERC721/ERC721.sol#L96)*** function in the ERC721 standard:
    
    ```solidity
    /**
     * @dev See {IERC721Metadata-tokenURI}.
     */
    function tokenURI(uint256 tokenId) public view virtual returns (string memory) {
        _requireMinted(tokenId);
    
        string memory baseURI = _baseURI();
        return bytes(baseURI).length > 0 ? string.concat(baseURI, tokenId.toString()) : "";
    }
    
    function _baseURI() internal view virtual returns (string memory){
        return "";
    }
    ```
    
    In this implementation, the ***[tokenURI](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9e3f4d60c581010c4a3979480e07cc7752f124cc/contracts/token/ERC721/ERC721.sol#L96)*** function uses the ***concat*** function to join together the ***baseURI*** and the ***tokenID*** into a single string, which is the unique URI for the NFT.
    

### Documentation

To concatenate a *string* we can use the `concat()` method.

```solidity
string str_1 = "hello ";
string str_2 = "world";

// result will be "hello world"
string result = string.concat(str_1, str_2);
```

The ***concat*** function will add the *string* *variables* and turn them into a single *string* *variable*.

### FAQ

- When should we use *string concatenation*?
    
    *String concatenation* is used whenever we need to combine multiple *strings* into a single *string*. Some common use cases include:
    
    - Building messages: When we need to generate a message that includes multiple pieces of information, we can use *string concatenatio*n to combine those pieces into a single message.
    - Formatting output: When we need to display output to the user, we can use *string* *concatenation* to format that output in a readable way. For example, we might *concatenate* a *string* and a number to display a balance as "*Your balance is 10 ETH*".

# Example/Example

```solidity
pragma solidity ^0.8.0;

contract StringExample {
  string public greeting = "Hello, ";
  string public name = "Alice";
    
  string result = string.concat(greeting, name);
    
  string public message;
  function setMessage() public {
    message = string.concat("Hello, ", name);
  }
}
```
