# Content/Define the Constructor

After defining our CryptoKitty *contract*, don't forget that ERC721 has a constructor that requires the token's name and symbol as parameters to initialize ERC721.

Next, we'll define our own *constructor* to *initialize* ERC721. 

**Syntax**

constructor

inherited

- hint
    
    ```solidity
    constructor() ERC721("name", "symbol") {}
    ```
    
