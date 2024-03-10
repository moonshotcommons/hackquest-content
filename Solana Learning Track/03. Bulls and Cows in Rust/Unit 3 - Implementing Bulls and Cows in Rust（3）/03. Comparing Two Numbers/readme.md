# Content/**Comparing Two Numbers**

After capturing the user's input, we can now proceed to the final step of the program – comparing two numbers.

### **Numerical Comparison**

We will use the ***cmp*** method and ***Ordering*** from the ***std*** library to implement the comparison functionality.

> cmp(): This method is *generic* and can be used to compare various types of values, such as **integers**, **strings**, **floating-point numbers**, **etc**.
> 

```rust
fn main() {
    let num1 = 42;
    let num2 = 30;

    // Use the cmp method to compare the sizes of two integers
    match num1.cmp(&num2) {
        std::cmp::Ordering::Less => println!("{} is less than {}", num1, num2),
        std::cmp::Ordering::Equal => println!("{} is equal to {}", num1, num2),
        std::cmp::Ordering::Greater => println!("{} is greater than {}", num1, num2),
    }
}
```

First, we declare two variables: `num1` and `num2`. We use the ***match()*** and ***cmp()*** methods to compare the two numbers. The cmp method returns an enumeration of `std::cmp::Ordering`, which has three variants: `Less`, `Equal`, and `Greater`. We use the ***match()*** expression to perform different operations based on the result of the comparison.