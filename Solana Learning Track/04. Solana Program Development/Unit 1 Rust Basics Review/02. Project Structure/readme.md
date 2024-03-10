# Content

Learning Objectives: Reviewing Rust project structure and dependency imports.

In Chapter 6.6, "Rust Project Structure" we introduced the concepts of module, crate, and package. Let's briefly review:

**`module`**: It is a unit used to organize and encapsulate code. It can contain functions, structs, enums, constants, traits, and other modules. Modules can be created in Rust using the `mod` keyword, and modules can be nested to form a module tree.

**`crate`**: In Rust, it is a compilation unit and can be either a **library crate** or a **binary crate**. A crate can contain one or more modules.

**`package`**: It is a project that includes one or more related crates. It is defined by a `Cargo.toml` file containing metadata, dependencies, and other configuration options about the project.

In simple terms, a module is a subset of a crate, and a crate is a subset of a package. In this section, we will focus on the use of modules and crates.

### Importing Dependencies

In Rust, a `crate` contains some common `modules`. If we want to access an `item` (which could be a function, struct, trait, etc.) within a module, we need to know its "path" (similar to navigating in a file system).

Consider the crate structure as a tree, where the crate is the base, modules are branches, and each branch can have submodules or project items as additional branches.

The path for a specific module or item is the name of each step from the crate to that module, separated by `::`. As an example, let's look at the following structure:

- The base crate is `solana_program`.
- `solana_program` contains a module named `account_info`.
- `account_info` contains a struct named `AccountInfo`.

So, the path for `AccountInfo` would be `solana_program::account_info::AccountInfo`.

Without any other keywords, we need to reference the entire path to use `AccountInfo` in the code. However, using the **`use`** keyword, we can bring an item into scope, making it reusable throughout the file without specifying the full path each time. You often see a series of `use` statements at the top of Rust files. Like this:

```jsx
use solana_program::account_info::AccountInfo
```