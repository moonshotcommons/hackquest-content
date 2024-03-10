# Content

**`module`**: A unit used to organize and encapsulate code. It can contain functions, structs, enums, constants, traits, and other modules. In Rust, modules are created using the `mod` keyword, and modules can be nested to form a module tree.

**`crate`**: In Rust, it is a compilation unit that can be either a **library crate** or a **binary crate** (their differences are explained in the FAQ). A crate can include one or more modules.

**`package`**: It is a project that contains one or more related crates. Defined by a `Cargo.toml` file, it includes metadata about the project, dependencies, and other configuration options. A package may contain a main crate (usually an executable) and zero or more library crates (usually dependencies).

- **Metaphor**
    
    We can liken a package (project) to an entire house, where the overall planning and design of the house are similar to the project's `Cargo.toml` file, defining project metadata and structure. The entire house consists of many components (crates), such as the kitchen, bedroom, living room, etc. Each room has its own furniture and functionality, like structs, enums, functions, etc., in a module.
    
- **Use Case**
    
    In Rust, a `crate` contains `modules` that can be shared across multiple projects. To access an item (such as a function, struct, enum, trait, constant, etc.) in a module, you need to know its path (similar to navigating in a file system). The path to a specific module or item is composed of the names of each step in the crate, separated by `::`. Consider the structure below:
    
    1. The root crate is `solana_program`.
    2. `solana_program` contains a module named `account_info`.
    3. The `account_info` module contains `AccountInfo`.
    
    Therefore, the path to `AccountInfo` is `solana_program::account_info::AccountInfo`. While you can use the full path in your code, it can be tedious. Hence, you can use the `use` keyword to bring it into scope, like `use solana_program::account_info::AccountInfo`.
    

### **Documentation**

The following code demonstrates the definition of a module.

```rust
// Define a module using mod, followed by the module name (my_module)
mod my_module {
    // Content of the module
    pub fn my_function() {
        // Function body
    }
}
```

### **FAQ**

**Q: Can you provide a detailed explanation of the concepts of library crate and binary crate in Rust?**

A: Library crates and binary crates are two different types of Rust projects. They are used for building libraries (to be referenced by other programs) and executable programs, respectively. Let's delve into their concepts and differences:

**Library Crate**: This type of Rust project is created using `cargo new --lib crate_name`. Its primary purpose is to provide functional code for other programs to reference. The code in a library crate is typically generic and reusable.

Organization: The code of a library crate is usually located in a file named `lib.rs`, which contains the main module of the crate. The code of a library crate can be referenced by other crates by adding the appropriate dependencies in the `Cargo.toml` file.

**Binary Crate**: This is another type of Rust project created using `cargo new project_name`. Its main purpose is to build executable programs. This crate can include multiple modules, with one module specified as the main entry point, often in a file like `main.rs`. The code in a binary crate is used to create standalone executable files.

Organization: The code of a binary crate typically resides in a file named `main.rs`, which contains the main function `main()`.

In summary, a library crate is used to build functional code for other programs to reference, often located in `lib.rs` and referenced by other crates. A binary crate is used to build executable programs, usually located in `main.rs` and resulting in a standalone executable file.

**Note:** In a Rust project, you can include both library crates and binary crates. For example, a project might include a library for providing general functionality and a binary for demonstration or testing. In such cases, the project's directory structure often includes `src/lib.rs` and `src/main.rs`.

# Example

The following example demonstrates the hierarchy of modules, building a crate, and ultimately forming a package. Through the hierarchical organization of modules, the code has good structure and readability.

```rust
// src/main.rs

// Main module, equivalent to the hall of the house
mod living_room {
     // Submodule, equivalent to the bedroom of the house
     mod bedroom {
         // The functions in the module are equivalent to the furniture in the bedroom
         pub fn sleep() {
             println!("Sleeping in the bedroom");
         }
     }

     // Submodule, equivalent to the kitchen of the house
     mod kitchen {
         // The functions in the module are equivalent to the equipment in the kitchen
         pub fn cook() {
             println!("Cooking in the kitchen");
         }
     }

     // Functions in the main module are equivalent to activities in the lobby
     pub fn relax() {
         println!("Relaxing in the living room");
         bedroom::sleep(); // Call the function in the bedroom module
         kitchen::cook(); // Call the function in the kitchen module
     }
}

// Main function, equivalent to the entrance of the entire house
fn main() {
     // Call the function in the living_room module
     living_room::relax();
}
```