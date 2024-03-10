# Content/Program declaration

In the previous lesson, we successfully imported the required libraries, laying the foundation for our *on-chain program*. Now, we are entering a crucial step: program declaration.

Program declaration is a vital part of program development, as it defines the program’s unique identifier, known as the *program_id*. This identifier plays a pivotal role throughout the program’s entire lifecycle.

### **Using the declare_id! Macro**

1. **Setting a Fixed Program Address**:
    - In Solana's Anchor framework, we use the `declare_id!` macro to declare the *unique identifier* for our program.
    - This macro allows us to specify a *fixed address*, ensuring that even after program upgrades, the program's address remains unchanged. This approach reduces complexity during upgrades, making program maintenance and updates more straightforward and efficient.

### Syntax

declare_id!

- hint
    
    ```rust
    //should be replaced with the fixed program address of your choice.
    declare_id!("YourFixedProgramId...");
    ```