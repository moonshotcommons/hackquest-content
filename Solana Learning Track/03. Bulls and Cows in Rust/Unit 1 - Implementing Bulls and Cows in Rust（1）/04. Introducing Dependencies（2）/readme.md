# Content/**Introducing Dependencies**

In our last lesson, we explored the fundamental concept of project dependencies. Now, let's proceed to introduce a dependency into your code.

### **Introducing a Dependency Library**

Suppose we want to use the ***rand*** library in our project to generate random numbers.

> ***rand*** is a library for generating random integers within a specified range, and we'll use it to create a random integer.
> 

Here are the steps and an example:

1. **Open the Cargo.toml**
    
    In the root directory of our previously created project ***bulls_and_cows***, locate and open this file.
    
2. **Add the Dependency**
    
    Under `[dependencies]`, add a new line specifying the ***rand*** library and its version *0.8*.
    

```toml
[package]
name = "bulls_and_cows"
version = "0.1.0"
edition = "2021"

[dependencies]
rand = "0.8"
```

With this simple step, **Cargo** will automatically download and compile the ***rand*** library the next time the project is built, making it available for use in the project.

- Dependency Versioning
    
    When specifying a dependency version, you can control the exact version used to ensure the stability of your project. In the example above, `"0.8"` indicates that we want to use version *0.8.x* of the ***rand*** library, where x is any minor version number. Cargo will select the latest compatible minor version.
    