# Content

**Arrays:** Collections that group multiple elements of the **same type** together. In Rust, there are two commonly used types of arrays. One is the static `array`, directly allocated in stack memory, providing fast access but with a fixed length. The other is the dynamic array `Vector`, allocated in heap memory, allowing dynamic growth but with a performance cost.

We previously mentioned "tuples" in earlier sections, and the most significant difference between arrays and tuples is that arrays contain elements of the **same type**.

In this section, we will focus on content related to "static arrays."

- **Metaphor**
    
    A static array is like a shopping basket, determining the number of items it can hold from the start. On the other hand, a dynamic array is like a shopping bag, flexible to expand based on shopping needs. However, both require that all items be of the same type.
    
- **Use Case**
    
    Solana addresses (represented by public keys) are typically a 32-byte array. You can create a new **`Pubkey`** instance from an array containing 32 bytes using the **`new_from_array`** method in the **`Pubkey`** struct.
    
    ```rust
    // solana_program::pubkey::Pubkey
    
    // pubkey_array is a u8 array with a length of 32
    pub const fn new_from_array(pubkey_array: [u8; 32]) -> Self {
        Self(pubkey_array)
    }
    ```
    

### Documentation

The following code demonstrates the syntax for creating static arrays in different ways:

```solidity
// Type inference by the compiler without specifying the element type
let a = [1, 2, 3, 4, 5];

// Explicitly specifying type and length with [type; length]
let b: [i32; 5] = [1, 2, 3, 4, 5];

// Initializing an array with a specific value repeated N times, c = [3,3,3,3,3]
let c = [3; 5];
```

### FAQ

# Example

Next, we will learn about the creation of arrays whose elements are non-basic types, array access, boundary crossing, and related content of two-dimensional arrays.

```solidity
fn main() {
     // array = [type; length] This syntax is OK for basic types such as i32, f64, bool, etc.
     let a = [3u8; 5]; // a = [3, 3, 3, 3, 3]

     // But for non-basic types such as String, you need to use the following method, because the basic type data is in the stack memory and can be copied directly.
     // Data of non-basic types is in heap memory and requires deep copying.
     let b: [String; 3] = std::array::from_fn(|_i| String::from("rust")); // b = ["rust","rust","rust"]

     let c = [9, 8, 7, 6, 5];
     // Direct access via subscript
     let first = c[0]; // first = 9
     let second = c[1]; // second = 8

     // If you access a non-existent element, the compiler will directly recognize it and give an error message.
     // let none_element = c[100];

     // arrays is a two-dimensional array, each element is an array, and the element type is [u8; 5]
		 // arrays = [[3, 3, 3, 3, 3],[9, 8, 7, 6, 5]]
     let arrays: [[u8; 5]; 2] = [a, c];
}
```