# Content

A **tuple** is a collection formed by combining elements of various types. It is a compound type, and its length and order are fixed. Tuples are defined using parentheses `()`, containing multiple values separated by commas `,`.

- **Metaphor**
    
    Think of a tuple as a shopping list. Suppose you go grocery shopping, and your shopping list may include items of different types, such as fruits, vegetables, and beverages. Each item is like a value in the tuple, and the entire shopping list is a tuple. The length of this shopping list is fixed; once the items are listed, you cannot freely add or remove items after checkout.
    
- Use Case
    
    Solana provides a method to compute [program-derived addresses](https://docs.solana.com/developing/programming-model/calling-between-programs#program-derived-addresses), and the return type of this method is a tuple:
    
    ```rust
    // solana_program::pubkey::Pubkey
    
    pub fn find_program_address(
        seeds: &[&[u8]],
        program_id: &Pubkey
    		// Returns a tuple, with the first element being the PDA public key address,
    		// and the second element being the corresponding bump seed
    ) -> (Pubkey, u8)
    ```
    

### Documentation:

Creating a tuple:

```rust
// Create a tuple with length 4, containing elements of different types
let tup: (i32, f64, u8, &str) = (100, 1.1, 1, "This is a tuple");

// Tuple members can also be another tuple
let tup2: (u8, (i16, u32)) = (0, (-1, 1));
```

### FAQ

# Example

We demonstrate in the following code how to destructure, access tuples, and use tuples as return values of functions.

```solidity
fn main() {
     // Create a tuple of length 4 and multiple different element types
     let tup: (i32, f64, u8, &str) = (100, 1.1, 1, "这是一个元组");
    
     // Deconstruct the tup variable and bind the second element to the variable x
     let (_, x, ..) = tup;
     println!("The value of x is: {}", x); //1.1

     // Use . to access the element at the specified index
     let first = tup.0;
     let second = tup.1;
     let third = tup.2;
     let fourth = tup.3;
     println!("The value of first is: {}, second is: {}, third is: {}, fourth is: {}", first, second, third, fourth);

     let s = String::from("hello, hackquest.");
     //The function return value is a tuple type
     let (s1, len) = calculate_length(s);
     println!("The length of '{}' is {}.", s1, len);
}

// len() returns the length of the string
fn calculate_length(s: String) -> (String, usize) {
     let length = s.len();

     (s, length)
}
```
