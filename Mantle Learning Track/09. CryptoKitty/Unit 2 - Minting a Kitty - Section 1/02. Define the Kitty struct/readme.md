# Content/Define the Kitty struct

Earlier, we added the first variable, ***_tokenIdCounter***, to our contract based on ERC721.

Next, we need another variable to represent the attributes of the kitty, including its genes, birth time, the TokenId of the kitty's mother and father, and the generation number.

To store the attributes of a kitty, we choose to use the struct data type, which is a data structure that can effectively store various attribute information of an object.

For simplicity, we use uint256 to represent all of these attributes.  

**Syntax**

struct

- hint
    
    ```solidity
    //For example, this struct represents the basic information of each student.
    struct Student {
      uint256 studentid;
      string name;
      uint256 classid;
    }
    ```
    
