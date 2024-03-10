# Content/Create Gen-0 kitties in Constructor

We've now completed the ***createKittyGen0*** function.

Next, we'll invoke the ***createKittyGen0*** function within the constructor. This ensures that users cannot arbitrarily create **gen-0 kitties** on their own.

Each invocation of this function will generate a new kitty with a unique gene.

Since breeding the next generation of kitty requires a pair of cats, we will call this function twice.

**Syntax**

function call

- hint
    
    ```solidity
    constructor() {
      createKittyGen0();
      createKittyGen0();
    }
    ```
    
