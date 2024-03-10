# Content/Annotation

In the previous lesson, we successfully defined the data structure of the ***Counter***, which is the core of our *counter program*. Next, our goal is to *initialize* it.

However, before initializing the counter, we need to clarify some prerequisites. For example:

- Where to store the counter's data?
    
    A dedicated account is needed to securely store the data of ***Counter***.
    
- Who has the authority to initialize this counter?
    
    Only authorized accounts should be able to perform this operation, thereby maintaining the security and integrity of the program.
    

To effectively address these questions and manage the initialization process, we can define a new ***Initialize*** struct to store the required information and rules.

In the Anchor, we can use the `#[derive(Accounts)]` annotation on this struct to stipulate which accounts are involved in the initialization process and their respective roles and requirements.

> For example, we can specify one *account* for storing the data of ***Counter*** and another *account* as the user performing the initialization operation. This way, the Anchor framework can automatically verify whether these *accounts* meet our set conditions, ensuring the correctness and security of the initialization process.
> 

Since *multiple accounts* are interacted with during the initialization process, the data of these *accounts* need to remain valid during the execution of the *program*. We can use `<'info>`.

- It marks the lifetime of all references (such as account data) in the struct.
- `<'info>` ensures that these references are valid throughout the lifetime of the ***Initialize*** struct. This means that as long as the ***Initialize*** struct exists, the account data within it can be safely accessed and used.

**Syntax**

#[derive(Accounts)]，<'info> ，Struct

- hint
    
    ```rust
    #[derive(Accounts)]
    pub struct Initialize<'info> {
        
    }
    ```