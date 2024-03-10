# Content

**Generics**: A powerful programming feature in Rust that allows writing reusable, generic code without hardcoding it for specific data types. The core idea of generics is parameterized types, which means using placeholders to represent data types when defining. For example, the data types like `Vec<T>`, `HashMap<K,V>`, and `Option<T>` used in previous chapters use `<T>` to denote a generic parameter (other characters like K or V can also be used), and `T` can be replaced with any specific data type when actually used. This flexibility makes the code more generic and enhances readability.

- **Metaphor**
    
    Imagine a USB interface, it's a universal connection standard that can connect various devices such as printers, keyboards, and mice. Regardless of the brand or model of the device, as long as it complies with the USB standard, it can connect to the computer. This is analogous to generics, which can adapt to the connection requirements of various different types of devices.
    
- **Use Case**

### Documentation

Suppose we have a function `largest` that finds the largest element in an array of type `i32`. Now, if we need it to support arrays of type `i64`, what do we do? Of course, adding a separate function with a parameter of type `i64` would work, but it's cumbersome as the logic is essentially the same except for the type difference.

```rust
// Finding the largest element in an array of type i32
fn largest_for_i32(list: &[i32]) -> i32 {
    let mut largest = list[0];

    for &item in list.iter() {
        if item > largest {
            largest = item;
        }
    }

    largest
}

// Finding the largest element in an array of type i64
// Other than the difference in parameter type and return value type,
// everything else is exactly the same as the previous function
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

Is there a better way? Certainly, generics can help us solve this problem. Abstracting the specific type as a generic `T`, as long as the elements inside support comparison, we can abstract the above two functions into a single generic function.

```rust
fn largest<T>(list: &[T]) -> T {
    let mut largest = list[0];

    for &item in list.iter() {
        // This is just for illustrative purposes, actual code would need to add generic constraints
        if item > largest {
            largest = item;
        }
    }

    largest
}
```

### FAQ

# Example

We demonstrate how to use generics in structures, enumerations, and methods in the following code.

```solidity
// 1. Generics are used in the structure, and the types of all members are T
struct Point1<T> {
     x: T,
     y: T,
}

// 2. Use generics in the structure, and members can have different types
struct Point2<T,U> {
     x: T,
     y: U,
}

// 3. Use generics in enumerations, and the Option enumeration returns a value of any type Some(T), or no value None
enum Option<T> {
     Some(T),
     None,
}

// 4. Using generics in the method, we implemented the method get_x for the structure Point1<T>, which is used to return the value of the x member
impl<T> Point1<T> {
     fn get_x(&self) -> &T {
         &self.x
     }
}

fn main() {
     // 1. Use generics in structures
     let int_point = Point1 { x: 5, y: 10 };
     let float_point = Point1 { x: 1.0, y: 4.0 };

     // 2. Use generics in structures
     let p = Point2{x: 1, y:1.1};

     // 3. Use generics in enumerations
     let option1 = Option::Some(1_i32);
     let option2 = Option::Some(1.00_f64);

     // 4. Use generics in methods
     let x = int_point.get_x();
}
```