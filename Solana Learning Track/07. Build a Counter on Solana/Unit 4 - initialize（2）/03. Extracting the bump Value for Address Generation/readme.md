# Content/**Receiving Parameter Information**

Following the previous steps, the next thing to do is to obtain the *bump value* used for generating the account address. This is a key step in ensuring that our ***Counter*** account's address is both unique and secure.

1. **Extracting the Bump Value for Address Generation**：
    
    To obtain the *PDA bump value* associated with the ***Counter*** account, we can use the special field `ctx.bumps`.
    
    ```rust
    ctx.bumps.counter;
    ```
    
    <aside>
    💡 `ctx.bumps` is used to store the bump values of all Program Derived Addresses (PDA) used in the contract call.
    
    </aside>
    

Through these two lessons, we have not only prepared the capability to modify the ***Counter*** account but also ensured the uniqueness and security of its address.

**Syntax**

ctx.bumps

- hint
    
    ```rust
    let bump = ctx.bumps.counter;
    ```