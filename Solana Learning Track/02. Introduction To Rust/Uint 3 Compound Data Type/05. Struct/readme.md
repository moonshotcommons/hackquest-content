# Content

**Structs:** A custom data type in Rust used to organize and store members of different types. It allows you to create a data structure with multiple fields, each having its own type and name, enhancing code readability and maintainability. Defined using the `struct` keyword.

*Further Reading:* Structs exist in many programming languages, though the specific implementations and syntax may vary. For example, C is one of the birthplaces of structs; C++ inherits structs from C and introduces classes, enhancing the capabilities of structs. Go has a concept of structs for defining data structures with related fields and methods but lacks classic object-oriented inheritance. While Java doesn't have the concept of structs, its Class features share similarities with structs, representing a core aspect of Java's object-oriented programming...

- **Metaphor**
    
    Suppose we want to represent information about a car. In Rust, we can use structs to define the car's properties (such as brand, model, color, production year, etc.). This car struct helps organize and construct relevant information about the car.
    
- **Use Case**
    
    In Solana, the `AccountInfo` struct is a crucial data structure in Solana smart contracts, used to access and manipulate account information within the contract.
    
    ```rust
    pub struct AccountInfo {
        /// Account public key for unique identification
        pub key: &Pubkey,
        /// Lamports count for the account, a reference-counted smart pointer allowing mutable references to be shared across multiple places
        pub lamports: Rc<RefCell<&mut u64>>,
        /// Data held by the account
        pub data: Rc<RefCell<&mut [u8]>>,
        /// Owner of this account, also an account
        pub owner: &Pubkey,
        /// Epoch when rent for this account needs to be paid next
        pub rent_epoch: Epoch,
        /// Whether the transaction is signed by the account's public key
        pub is_signer: bool,
        /// Indicates whether the account is writable; if true, allows modification of account data
        pub is_writable: bool,
        /// Whether the account is an executable program
        pub executable: bool,
    }
    ```
    

### Documentation

Using cars as an example, let's learn how to define a struct: `struct` keyword + `Car` struct name + clear and concise fields with types.

```solidity
struct Car {
    // Brand
    brand: String,
    // Color
    color: String,
    // Production Year
    year: String,
    // Is it a new energy vehicle?
    is_new_energy: bool,
    // Price
    price: f64
}
```

### FAQ

- **Q: What are Tuple Structs, and when are they suitable?**
    
    A: Structs must have names, but their fields can be unnamed, resembling tuples. Such structs are called Tuple Structs.
    
    If you want an overall name but don't care about the individual field names, Tuple Structs are useful. For example, the `Point` tuple struct below: knownly, 3D points are in `(x, y, z)` format, so we don't need to name each field as `x`, `y`, `z`.
    
    ```rust
    // Only structure name: Color, no field name
    struct Color(i32, i32, i32);
    // Only structure name: Point, no field name
    struct Point(i32, i32, i32);
    
    let black = Color(0, 0, 0);
    let origin = Point(0, 0, 0);
    ```
    

# Example

Next, we learn the relevant syntax for creating, accessing, and updating structures.

```solidity
//Standard creation method
fn build_car(color: String, year: String, price: f64) -> Car {
     Car {
         brand: String::from("Tesla"),
         color: color,
         year: year,
         is_new_energy: true,
         price: price,
     }
}

//Simplified creation method
fn build_car2(color: String, year: String, price: f64) -> Car {
     Car {
         brand: String::from("Tesla"),
         // When the function parameters and structure fields have the same name, they can be initialized directly using abbreviation.
         color,
         year,
         is_new_energy: true,
         price,
     }
}

fn main() {
     // Declare Car type variable (requires variable must be mut type)
     let mut car1 = build_car2(String::from("black"), String::from("2023-01-01"), 123.00);

     //Access and modify the structure (accessed through the . operator)
     car1.color = String::from("white");
     println!("car1 {:?}", car1);

     // Create a new structure instance based on the existing structure instance
     let mut car2 = Car {
         color: String::from("greey"),
         //Other fields are taken from car1, ..car1 must be used at the end of the structure
         ..car1
     };

     println!("car2 {:?}", car2);
}
```