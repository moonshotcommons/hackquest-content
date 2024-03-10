# Content/**Dependencies**

In our previous lesson, we learned how to use Cargo to create a new Rust project. Now that you have a fresh, blank project, let's delve into how to **add dependencies** to it before we start coding.

### **What are Dependencies?**

In software development, dependencies are akin to the tools and materials in your toolbox. They are *reusable code libraries* written by other developers that add specific functionalities or performance enhancements to your project, saving you from writing repetitive code from scratch. Dependencies make development faster and more efficient, allowing you to focus on the core features of your project.

### **Managing Dependencies: Cargo.toml**

Let's revisit the file directory of the newly created project from the last lesson:

```bash
├── .git
├── .gitignore
├── Cargo.toml
└── src
    └── main.rs
```

In the root directory, there's a file named `Cargo.toml`, which contains information about the **project** and **its dependencies**.

```bash
[package]
name = "bulls_and_cows"
version = "0.1.0"
edition = "2021"

[dependencies]
```

1. [package]：This section records the *metadata* of the project. `name` is the project name, `version` is the project version number, and `edition` specifies the Rust language edition.
2. [dependencies]：This section lists the *project's dependencies*, indicating which external libraries and their versions are required for your project.