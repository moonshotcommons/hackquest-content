# Content

**Variable destructuring** is a process of breaking down values from composite data types (such as tuples, structs, enums, etc.) into individual variables. It allows for the extraction of needed values from complex data structures in a convenient and concise manner. This approach enhances control over data visibility and contributes to more elegant code.

In simpler terms, variable destructuring is akin to unwrapping a known structure. It is not unique to Rust and is present in many programming languages like Python, JavaScript, Solidity, and more.

- **Metaphor**
    
    Variable destructuring is a method of extracting information from complex data structures. Imagine having a basket filled with various fruits—bananas, pineapples, and durians. Each fruit in the basket corresponds to an element in a tuple. With variable destructuring, you can place each type of fruit in different plates. Of course, if you don't like durians, you can choose to only put bananas and pineapples on the plates. Variable destructuring shares a philosophical connection with ***Occam's Razor***; it allows us to focus only on the variables we need in complex data types, ignoring the rest—doesn't this align with the principle of "entities must not be multiplied beyond necessity"?
    
- **Use Case**
    
    In Solana, the `find_program_address` function calculates a PDA (Program Derived Account), account derived from the main program and do not have a private key. The function returns a tuple with two elements, and we can decide whether to accept the second element based on our needs:
    
    ```rust
    // Calculate PDA account and bump seed based on an array of signer keys and program ID
    let (pda_account, bump_seed) = Pubkey::find_program_address(&[signer.key.as_ref()], program_id);
    
    // If the second element is not needed, it can be replaced with _
    let (pda_account, _) = Pubkey::find_program_address(&[signer.key.as_ref()], program_id);
    ```
    

### Documentation

We can use the following approaches to place bananas, pineapples, and durians in three different plates, or alternatively, only take bananas and pineapples.

```rust
// First approach
let (a, b, c) = ("Banana", "pineapple", "durian");

// Second approach
let (e, d, _) = ("Banana", "pineapple", "durian");

```

### FAQ

- **Q: Which complex data types are commonly suited for variable destructuring?**
    
    A: Variable destructuring is commonly applied to the following types:
    
    1. **Tuple Types:** Combines multiple values of different types into a single data structure, for example, `(1, "hello", 3.14)`.
    2. **Array Types:** Groups multiple values of the same type into a single data structure, for example, `[1, 2, 3, 4]`.
    3. **Struct Types:** A custom data type that combines different types of data to form a new structure. For instance:
        
        ```rust
        // An adorable little crab
        struct Ferris {
            id_number: i32,
            name: String,
        }
        
        ```
        
    
    In subsequent chapters, we will provide dedicated introductions to these types. For now, it's good to have a preliminary understanding.
    

# Example

We demonstrate how to perform destructuring assignment through the data types of tuples, arrays, and structures, and only obtain the fields we care about. (These data types will be introduced in detail in Chapter 3)

```solidity
struct Ferris {
    e: i32,
    f: String
}

fn main() {
    let (a, b, c, d, e, f);

    // tuple destructure
    (a, b) = (1, 2);
    // Array destructuring, .. means ignoring multiple elements, _ means ignoring the element at the corresponding index position (1)
    [c, .., d, _] = [1, 2, 3, 4, 5];
    // struct destructure
    Ferris { e, f } = Ferris { e:5, f:"rust".to_string() };

    assert_eq!((1, 2, 1, 4, 5, "rust".to_string()), (a, b, c, d, e, f));
}
```