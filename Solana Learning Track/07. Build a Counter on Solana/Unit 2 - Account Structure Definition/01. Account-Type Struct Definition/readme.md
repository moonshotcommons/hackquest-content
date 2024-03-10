# Content/Account-Type Struct Definition

In the previous lesson, we have already imported the libraries necessary for the contract. Next, we begin writing the contract.

First, we need a data structure to store our counter information. To efficiently store count information, using a struct to organize the data is a good choice.

To facilitate the management and updating of the ***Counter*** state, we will design ***Counter*** as a separate data account. This approach has several important benefits:

1. **Data Persistence**:
    
    As a data account, the state of ***Counter*** will be persistently stored on the blockchain. This means that whenever the program is called, the information of ***Counter*** is up-to-date and consistent.
    
2. **Security and Independence**:
    
    Designing ***Counter*** as an independent account also enhances data security and the robustness of the contract, ensuring that the program’s state is not affected by the operations of other programs.
    

In the Anchor framework, we use the `#[account]` attribute, which helps us mark the ***Counter*** struct as a data account.

**Syntax**

#[account] ，struct

- hint
    
    ```rust
    #[account]
    pub struct Student{
        pub id: u64,
    }
    ```