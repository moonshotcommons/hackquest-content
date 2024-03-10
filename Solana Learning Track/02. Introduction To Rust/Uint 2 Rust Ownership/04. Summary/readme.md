# Content

Building upon the concepts learned in the previous sections, let's delve deeper into ownership in functions, drop details, and the limitations of mutable borrowing.

- **Metaphor**
- **Use Case**
    
    In Solana programs, we can obtain and modify data from an account using the following approach:
    
    ```rust
    // borrow_mut returns the type RefCell, commonly used when borrowing rules are not determinable at compile time
    // [..] gets the complete slice of data
    let data: &mut [u8] = &mut account.data.borrow_mut()[..];
    data[0] = instruction_data[0];
    ```
    

### Documentation:

Ownership can be transferred to functions. During the transfer, the owner's stack values will be copied to the parameter stack of the function call.

```rust
struct Foo {
    x: i32,
}

fn do_something(f: Foo) {
    println!("{}", f.x);
    // f is dropped (released) here
}

fn main() {
    let foo = Foo { x: 42 };
    // foo is transferred to do_something
    do_something(foo);
    // After this point, foo can no longer be used
}
```

Of course, ownership can also be acquired from functions:

```rust
fn do_something() -> Foo {
    Foo { x: 42 }
    // Ownership is moved out
}

fn main() {
    let foo = do_something();
    // foo becomes the owner
    // foo is dropped at the end of the function scope
}
```

- **FAQ**:
    
    **Q: What is drop by levels?**
    
    A: Taking a struct as an example, when removing a struct, the struct itself is released first, followed by the respective release of its sub-structs, and so on.
    
    ```rust
    struct Bar {
        x: i32,
    }
    
    struct Foo {
        bar: Bar,
    }
    
    fn main() {
        let foo = Foo { bar: Bar { x: 42 } };
        println!("{}", foo.bar.x);
        // foo dropped first
        // foo.bar dropped second
    }
    ```
    

# Example

After a mutable borrow occurs, the owner of a resource cannot be borrowed or modified again. This is done to avoid potential data races.

```solidity
struct Foo {
     x: i32,
}

fn do_something(f: Foo) {
     println!("{}", f.x);
     // f is dropped here and released
}

fn main() {
     let mut foo = Foo { x: 42 };
     let f = &mut foo;

     // An error will be reported: do_something(foo);
     // Unable to take ownership of foo because it has been mutably borrowed

     // An error will be reported: foo.x = 13;
     // Because foo has been mutably borrowed and cannot be modified

     f.x = 13;
     // f will be dropped because it will no longer be used.
    
     println!("{}", foo.x);
    
     // Now modifications can proceed normally because all mutable references have been dropped
     foo.x = 7;
    
     //Move ownership of foo into a function
     do_something(foo);
}
```