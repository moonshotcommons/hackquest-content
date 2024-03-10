# Content

> In previous sections, we learned about Rust's data types such as structs, enums, and methods. We also understood that methods define the behavior of a type, and in this section, we will introduce a new concept: Traits.
> 

**Trait:** A type's behavior is composed of the methods it can call. If different types can be called with the same method, they can share common behavior. `Trait` is a mechanism that combines method signatures to build a collection of behaviors necessary for a specific purpose. In essence, it defines shared behavior for a type and abstracts the implementation of code.

- **Metaphor**
    
    Let's use the analogy of geese and swallows. They have their own behaviors; for example, geese settle by the lake, and swallows build nests under the eaves. This is similar to Rust's **methods**. At the same time, they both belong to migratory birds, exhibiting the **southward migration** behavior. We can abstract this common behavior as a **`Trait`** and provide their respective implementations. For instance, geese migrate in a V-shaped formation, while swallows fly rapidly close to the ground, hovering in flight. Therefore, a Trait is an abstraction of type methods, allowing for better management of Rust objects.
    
- **Use Case**
    
    In Solana, there is a `Trait` named `Account`, where the `get` method provides metadata for constructing `AccountInfo`.
    
    ```rust
    // solana_program::account_info::Account
    
    pub trait Account {
        // Required method
        // Returns: lamports, data, owner, executable, rent_epoch
        fn get(&mut self) -> (&mut u64, &mut [u8], &Pubkey, bool, Epoch);
    }
    ```
    

### Documentation

Here, we demonstrate how to define a `Trait` and implement related logic on a struct.

```rust
// trait keyword + migrant_bird trait name
trait MigrantBird {
    // Define a method for this trait; the parameter must include &self since it is a behavior of this type
    fn migrate(&self) -> String;
}

// Define the struct for wild geese
struct WildGoose {
     color: String,
}

// Implement the MigrantBird trait for the WildGoose type
impl MigrantBird for WildGoose {
     fn migrate(&self) -> String {
         "Geese fly in a V-shaped formation".to_string()
     }
}
```

> Note: If a Trait method does not have a default implementation, the method definition ends with a semicolon `;`. This means it only has a method signature, without `{}`for the method body, as the specific implementation is left to the responsibility of each type.
> 

### FAQ

**Q: What is the default implementation of a `Trait`?**

A: Since a `Trait` is about shared behavior, we can assign default behavior to it, and types can override it when necessary or use the default behavior. The code below shows how to define default behavior.

```rust
// default implement: default_migrant
trait MigrantBird {
    fn default_migrant(&self) {
        println!("i am flying to the warm south");
    }
}

struct Swallow {
    color : String,
}

// use defualt implement
impl MigrantBird for Swallow {}

fn main() {
    let small_swallow = Swallow {
        color : String::from("black")
    };
    small_swallow.default_migrant();
}
```

# Example

Here we define `WildGoose` and `Swallow` structures, which have their own methods. At the same time, there is also a common method of migrating south, namely `Trait`: `migrant`.

```solidity
struct WildGoose {
     color: String,
}

// WildGoose's own method
impl WildGoose {
     //Create an instance of itself
     fn new() -> Self {
         WildGoose {
             color: "gray".to_string(),
         }
     }
// Perch by the lake
     fn inhabit(&self) {
         println!("wild geese perch by the lake");
     }
}

// Swallow structure
struct Swallow {
     color: String,
}

// Swallow's own method
impl Swallow {
     fn new() -> Self {
         Swallow {
             color: "black".to_string(),
         }
     }
// Build a nest under the eaves
     fn build_nest(&self) {
         println!("swallows build nests under the eaves")
     }
}

// trait
trait MigrantBird {
     //Leave it to the respective types to implement
     fn migrant(&self) -> String;
}

// Implement the migrant method of Trait feature for WildGoose
impl MigrantBird for WildGoose {
     fn migrant(&self) -> String {
         "Geese fly in a V-shaped formation".to_string()
     }
}

// Implement the migrant method of Trait for Swallow
impl MigrantBird for Swallow {
     fn migrant(&self) -> String {
         "swallow fly fast, but have to rest frequently".to_string()
     }
}
```