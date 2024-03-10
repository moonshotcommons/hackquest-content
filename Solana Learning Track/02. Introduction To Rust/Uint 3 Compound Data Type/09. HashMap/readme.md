# Content

**HashMap:** In Rust, a collection type used to store key-value pairs. Each key (`key`) maps to a value (`value`), and each key must be unique. This structure allows us to quickly retrieve a value by its key without having to iterate through the entire collection. The efficiency of HashMap comes from its hash function, which converts keys into indices for direct memory access, significantly speeding up the lookup process.

- **Metaphor**
    
    The HashMap data structure is analogous to a real-world library: each book (value) has a unique call number (key). Librarians can quickly find the specific location of a book in the library's computer system (HashMap) by using its call number. This is much faster than searching through each bookshelf because the system internally uses the call number to locate the book, similar to how HashMap uses keys to locate values.
    
- **Use Case**
    
    Hash functions are crucial not only in HashMaps but also in the blockchain domain. In Solana, an account's address is obtained by applying the SHA-256 and Keccak (SHA-3) hash functions to the account's public key, and the result is finally encoded using Base58 (removing easily confused characters like 0, o, 1, l) for representation.
    

### Documentation

You can create a HashMap using the following two methods. If you know the number of key-value pairs in advance, creating a HashMap with a specified size can be more efficient to avoid frequent memory allocation and copying, thus improving performance.

```rust
// Since HashMap is not included in Rust's prelude library, it needs to be manually imported.
use std::collections::HashMap;

fn main() {
    // Create a HashMap to store student grades
    let mut student_grades = HashMap::new();
    student_grades.insert("Alice", 100);

    // Create a HashMap with a specified size to avoid frequent memory allocation and copying, improving performance.
    let mut student_grades2 = HashMap::with_capacity(3);
    student_grades2.insert("Alice", 100);
    student_grades2.insert("Bob", 99);
    student_grades2.insert("Eve", 59);
}
```

### FAQ

# Example

Through the following examples, we will learn how to convert an array into a HashMap, as well as query, traverse, change and other operations of HashMap.

```solidity
use std::collections::HashMap;
fn main() {
     // Vector, type is tuple (user, balance)
     let user_list: Vec<(&str, i32)> = vec![
         ("Alice", 10000),
         ("Bob", 1000),
         ("Eve", 100),
         ("Mallory", 10),
     ];

     // Use iterator and collect method to convert array to HashMap
     let mut user_map: HashMap<&str, i32> = user_list.into_iter().collect();
     println!("{:?}", user_map);

     // Get the corresponding value through hashmap[key]
     let alice_balance = user_map["Alice"];
     println!("{:?}", alice_balance);

     // Get the corresponding value through hashmap.get(key), and the return value is the Option enumeration type
     let alice_balance: Option<&i32> = user_map.get("Alice");
     println!("{:?}", alice_balance);

     // If the key does not exist, the return value is None, but no error will be reported.
     let trent_balance: Option<&i32> = user_map.get("Trent");
     println!("{:?}", trent_balance);

     // Overwrite the existing value, insert operation returns the old value
     let old = user_map.insert("Alice", 20000);
     assert_eq!(old, Some(10000));

     // or_insert returns a reference to the old value if it exists; if it does not exist, inserts the default value and returns its reference
     let v = user_map.entry("Trent").or_insert(1);
     assert_eq!(*v, 1); // Does not exist, insert 1

     // Verify the value corresponding to Trent
     let v = user_map.entry("Trent").or_insert(2);
     assert_eq!(*v, 1); // Already exists, so 2 is not inserted
}
```