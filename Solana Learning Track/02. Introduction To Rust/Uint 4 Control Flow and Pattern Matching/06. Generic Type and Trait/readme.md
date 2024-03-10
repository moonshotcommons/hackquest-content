# Content

Generic monomorphization is a compilation optimization technique that transforms generic code into specific code by filling in concrete types used at compile time. In contrast to the steps of creating generic functions, the compiler looks for all the places where generic code is invoked and generates code specifically for those instances using concrete types.

- Metaphor
- Use Case
    
    Let's take Solana's `AccountInfo` as an example, which implements the `From` trait. This trait supports generics:
    
    ```rust
    // The From trait implements type conversion, and here it is generic over T, supporting conversion for various types
    pub trait From<T>: Sized {
        // Required method
        fn from(value: T) -> Self;
    }
    
    // IntoAccountInfo is also a trait, here it is essentially implementing the From trait for the IntoAccountInfo type,
    // ultimately obtaining data of the AccountInfo type
    impl<T: IntoAccountInfo> From<T> for AccountInfo {
        fn from(src: T) -> Self {
            src.into_account_info()
        }
    }
    ```
    

### Documentation

Expanding on the generic function `largest` from the previous section, where the parameter type is `&T`, allowing the function to be called with `i32`, `i64`, or other types.

```rust
// T can represent any type
fn largest<T>(list: &[T]) -> T {
    let mut largest = list[0];
    for &item in list.iter() {
        if item > largest {
            largest = item;
        }
    }

    largest
}

fn main() {
    let arr1: [i32; 3] = [1, 2, 3];
    largest(&arr1);
    let arr2: [i64; 3] = [1, 2, 3];
    largest(&arr2);
}
```

However, during compilation, for each case where the generic function is used with different types, the compiler generates a specific function for better performance. The monomorphized code looks similar to this:

```rust
// Re-instantiated function for i32 type
fn largest_for_i32(list: &[i32]) -> i32 {
    let mut largest = list[0];
    for &item in list.iter() {
        if item > largest {
            largest = item;
        }
    }
    largest
}

// Re-instantiated function for i64 type
fn largest_for_i64(list: &[i64]) -> i64 {
    let mut largest = list[0];
    for &item in list.iter() {
        if item > largest {
            largest = item;
        }
    }
    largest
}
```

In summary, we can use generics to write non-repetitive code, and Rust will compile specific code for each instance. This means there is no runtime overhead when using generics; The code's execution efficiency is similar to hand-writing repetitive code for each specific definition. This monomorphization process is why Rust generics are highly efficient at runtime.

### FAQ

**Q: What is a Trait bound?**

A: Let's look at how a `Trait` is passed as a parameter. Going back to the example of the migratory bird `MigrantBird` from the previous section, we defined a method `fly` with a parameter type of `MigrantBird` as follows:

```rust
// Trait
trait MigrantBird {
    fn migrate(&self) -> String;
}

// Implementing the MigrantBird trait for WildGoose
impl MigrantBird for WildGoose {
    fn migrate(&self) -> String {
        "Geese fly in a V-shaped formation".to_string()
    }
}

// Implementing the MigrantBird trait for Swallow
impl MigrantBird for Swallow {
    fn migrate(&self) -> String {
        "swallow fly fast, but have to rest frequently".to_string()
    }
}

// Function with Trait as a parameter
fn fly(item: impl MigrantBird) {
    println!("I am flying to the warm south");
}

```

Of course, for the `fly` method, we can also implement it using a `Trait bound`. This way, only parameters of type `MigrantBird` can call the function. In other words, we restrict the generic type of the parameter to be of type `MigrantBird`.

```rust
fn fly<T: MigrantBird>(item: T) {
		println!("i am flying to the warm south");
}
```

# Example

In the body of the `largest` function we want to compare two values of type `T` using the greater than operator (`>`). This operator is defined as a default method of the trait `std::cmp::PartialOrd` in the standard library. Therefore, `PartialOrd` needs to be specified in the trait bound of `T`, as follows:

```solidity
// 1. Implement the feature constraints of PartialOrd
fn largest<T: PartialOrd>(list: &[T]) -> T {
     let mut largest = list[0];
     for &item in list.iter() {
//Only if the PartialOrd feature is implemented, the size can be compared
         if item > largest {
             largest = item;
         }
     }

     largest
}

// For the above code, compilation still fails because the list[0] operation attempts to move the element to the largest variable,
// Only types that implement the Copy attribute can do this, and for values of non-Copy types, ownership will result
// transfer

// 2. Implement the characteristic constraints of copy
fn largest<T: PartialOrd + Copy>(list: &[T]) -> T {
     let mut largest = list[0];
     for &item in list.iter() {
         if item > largest {
             largest = item;
         }
     }

     largest
}

// 3. Implement feature constraints through where
fn largest<T>(list: &[T]) -> T
where T: PartialOrd + Copy,
{
     let mut largest = list[0];
     for &item in list.iter() {
         if item > largest {
             largest = item;
         }
     }

     largest
}
```