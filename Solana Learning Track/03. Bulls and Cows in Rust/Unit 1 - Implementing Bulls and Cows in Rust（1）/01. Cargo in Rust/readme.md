# Content/**What is Cargo**

Cargo is the package manager and build system for the Rust programming language. 

<aside>
💡 Just as you need tools and materials to build a building, Cargo provides all the tools and libraries you need for Rust project development.

</aside>

Cargo helps you from creating a project, downloading project dependencies, compiling code, building, and testing, to finally running and deploying your project.

### **How to Install Cargo**

- If we have already installed Rust, Cargo will be installed along with it, so there's no need for additional installation.
- If you haven't installed the Rust environment yet, you can follow these tutorials for installation: **[Install Rust](https://course.rs/first-try/installation.html#%E5%AE%89%E8%A3%85-rust)** or **[Rust Install](https://www.rust-lang.org/tools/install)**

### **Related Commands**

Whether you're a beginner or a seasoned developer, Cargo will be an indispensable tool in your Rust development. Of course, if you're not familiar with it, don't worry. Next, let's learn about Cargo's related commands.

- basic commands
    
    ```bash
    cargo new (project's name)  // Create a new cargo project
    cargo build                 // Compile the project
    cargo run                   // Compile the project and then run it
    ```
    
- other commands
    
    We can run the `cargo -h` in the command line tool to view all of Cargo's commands and their descriptions.
    
    ```jsx
    		clean       Remove the target directory
        doc, d      Build this package's and its dependencies' documentation
        new         Create a new cargo package
        init        Create a new cargo package in an existing directory
        add         Add dependencies to a manifest file
        remove      Remove dependencies from a manifest file
        run, r      Run a binary or example of the local package
        test, t     Run the tests
        bench       Run the benchmarks
        update      Update dependencies listed in Cargo.lock
        search      Search registry for crates
        publish     Package and upload this package to the registry
        install     Install a Rust binary. Default location is $HOME/.cargo/bin
        uninstall   Uninstall a Rust binary
    ```