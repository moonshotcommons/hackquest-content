# Content/Define Struct

Every *contract* is about something: Tokens, books, students, courses. No matter what it is, we need a **data structure** that could represent it. 

It’s the same here with NFT. We need a data structure to store detailed information about the **NFT**, such as name, description, and owner.

Struct is the most suitable data type here because it groups related information together as we mentioned in Struct Lesson in Syntax. 

**Syntax**

value types

- hint
    
    ```solidity
    contract Example{
      //Define the Apple structure to store Apple's information
      struct Apple {
        string name;        // Apple name
        string description; // Apple description
        address owner;      // Apple owner's address
      }
    }
    ```