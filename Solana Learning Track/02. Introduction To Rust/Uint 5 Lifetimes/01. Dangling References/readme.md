# Content

Target : Understand the concepts and principles of dangling references.

A **dangling reference** occurs when attempting to use a reference to a value that has gone out of scope. In earlier chapters, we introduced the concept of **borrowing**, which involves obtaining a **reference** to a **value**. However, if the value is deallocated by Rust's memory manager (dropped) after leaving its scope, and an attempt is made to use that reference, it results in a dangling reference error.

- Metaphor
    
    Dangling references can be likened to someone lending money and then passing away. The question arises: should the borrower still repay the debt? If not, then it seems everyone borrowing money would hope the lender passes away soon, introducing societal instability. If yes, then how should the repayment happen? This is similar to a situation in Rust where a reference to a value is created, and later that value is deallocated. Therefore, the original reference points to a non-existent value—a dangling reference. In society, such issues are resolved through legal regulations, while in Rust, the borrow checker in the compiler addresses dangling references.
    
- Use Case

### Documentation

```rust
// Let's look at an example of a dangling reference.
{
    let r;
    {
        let x = 5;
        r = &x;
    }
    println!("r: {}", r);
}
```

In this example, the variable `x` has its scope within the inner `{}`. At this point, the variable `r` receives a reference to `x`. However, after the inner `{}`, Rust deallocates the variable `x`. Since the scope of the variable `r` extends to the outer `{}`, it remains valid. But, its value is no longer present. Consequently, variable `r` becomes a dangling reference, leading to a compilation error with the message `x does not live long enough, borrowed value does not live long enough`.

### FAQ

**Q1: How does the borrow checker work?**

A: The Rust compiler includes a borrow checker that compares the scopes to ensure all borrows are valid. For the example above, the borrow checker annotates the scope ranges as follows:

```rust
{
    let r;                // ---------+-- 'a
                          //          |
    {                     //          |
        let x = 5;        // -+-- 'b  |
        r = &x;           //  |       |
    }                     // -+       |
                          //          |
    println!("r: {}", r); //          |
}

```

Here, we observe that the scope of variable `r` is indicated by `'a`, and the scope of variable `x` is marked by `'b`. The scope 'b is smaller than 'a, implying that the value's scope is smaller than the reference's scope. The borrow checker identifies this situation as a potential issue with the validity of the reference.

**Q2: How can the example be modified to pass the borrow checker's check?**

A: It is sufficient to ensure that the value's scope `'b` is greater than the reference's scope `'a`. In other words, as long as the lender (value) is alive, Rust's world considers the borrowing to be allowed.

```rust
{
    let x = 5;            // ----------+-- 'b
                          //           |
    let r = &x;           // --+-- 'a  |
                          //   |       |
    println!("r: {}", r); //   |       |
                          // --+       |
}                         // ----------+

```

# Example

There will be more complex reference relationships in the function, that is, it may have dangling references, or it may not, in which case the borrow checker will not work. Below is a piece of pseudo code just to illustrate the scenario of dangling references in functions.

```solidity
// Get the longest of the strings referenced by variables x and y
fn longest(x: &str, y: &str) -> &str {
     if x.len() > y.len() {
         x
     } else {
         y
     }
}

// result points to a reference to string2, but the scope of this reference is limited to the inner {}, so a dangling reference will occur during println.
fn main1() {
     let string1 = String::from("123456789");
     let result;
     {
         let string2 = String::from("abcdefghijklmnopqrstuvwxyz");
         result = longest(string1.as_str(), string2.as_str());
     }
     println!("The longest string is {}", result);
}

// The values of string1 and string2 are exchanged here. At this time, result1 points to the reference of string1. Since the scope of the value of string1 is greater than the scope of the reference,
// In theory, this code can be compiled successfully, but in practice it will still fail to compile.
fn main2() {
     let string1 = String::from("abcdefghijklmnopqrstuvwxyz");
     let result;
     {
         let string2 = String::from("123456789");
         result = longest(string1.as_str(), string2.as_str());
     }
     println!("The longest string is {}", result);
}

// Summary: Rust's compiler is not as smart as humans. On the contrary, it is more conservative than humans. Therefore, for the above code, there must be a clear mechanism to identify the scope.
// Otherwise, Rust will fail to compile.
```