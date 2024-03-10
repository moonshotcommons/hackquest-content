# Content/Create an NFT

After defining the *function header*, it’s time to actually implement the *function*.

To mint an NFT, we need to first create it, and then **update** every related data structure. 

In specific, we define a new *variable* in the ***Token***, because all of our NFTs are represented using the ***Token***.

**Syntax Review**

struct

- hint
    
    ```solidity
    Book newone = Book(_d, _n);
    ```