# Content

In the previous sections, we gained some understanding of strings. Now, we will continue learning about various string operations such as appending, inserting, replacing, and deleting.

- **Metaphor**
    
    Strings can be compared to trains composed of carriages. We can perform various operations on the train, such as increasing capacity by coupling two trains together. If a carriage is damaged, we can detach it, repair it, and then insert it back or directly attach it to the end of the train.
    
- **Use Case**

### Documentation:

A **string** is a continuous collection of **characters**. In Rust, characters use the Unicode character set, with each character conventionally taking up 4 bytes. However, Rust adopts `UTF-8` encoding for strings, meaning the number of bytes each character occupies can vary (1 - 4 bytes). This design helps significantly reduce the memory footprint of strings.

```rust
let say = String::from("hello,世界");
// Length is 12
// UTF-8 uses 1 byte for ASCII characters and 3 bytes for common Chinese characters
println!("Length: {}", say.len());
```

### FAQ:

- **Q: What is the difference between bytes, characters, and strings?**
    
    A: **Bytes** are a unit of length and occupy 8 bits in the computer, regardless of the programming language. **Characters** represent single characters in text and are denoted by the `char` type in Rust. **Strings** are sequences of characters, and in Rust, the string type is `String`.
    

# Example

Next, we introduce Push, insert , replace , and delete operations of strings

```solidity
fn main() {
     let mut s = String::from("Hello ");

     // Append a string, modify the original string, not generate a new string
     s.push_str("rust");
     println!("Append string push_str() -> {}", s);

     //Append characters
     s.push('!');
     println!("Append character push() -> {}", s);

     //Insert characters and modify the original string. You need to specify the index position. The index starts from 0.
     // If it goes out of bounds, an error will occur
     s.insert(5, ',');
     println!("Insert character insert() -> {}", s);

     //Insert string
     s.insert_str(6, "I like");
     println!("Insert string insert_str() -> {}", s);

     // replace The replacement operation generates a new string. Requires 2 parameters, the first parameter is
     // The string to be replaced, the second parameter is the new string
     let str_old = String::from("I like rust, rust, rust!");
     let str_new = str_old.replace("rust", "RUST");
     println!("The original string length is: {}, memory address: {:p}", str_old, &str_old);
     println!("The new string length is: {}, memory address: {:p}", str_new, &str_new);

     // pop delete operation, modify the original string, which is equivalent to popping the last character of the character array
     //The return value is the deleted character, Option type, if the string is empty, None is returned
     // Note: pop is performed according to the "character" dimension, not "byte"
     let mut string_pop = String::from("删除操作，rust 中文!");

     // What is deleted at this time is the exclamation mark "!" at the end.
     let p1 = string_pop.pop();
     println!("p1:{:?}", p1);
     // Delete the "文" at the end based on p1
     let p2 = string_pop.pop();
     println!("p2:{:?}", p2);
     //The remaining string at this time is “删除操作，rust 中”
     println!("string_pop:{:?}", string_pop);
}
```