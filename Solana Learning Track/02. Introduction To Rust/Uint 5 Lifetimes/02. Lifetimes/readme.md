# Content

**Lifetimes :** In Rust, every **reference** has a **lifetime** associated with it, indicating the duration for which the reference remains valid. In most cases, we don't need to manually declare lifetimes because the compiler can automatically infer them. However, when dealing with multiple lifetimes, as in the previous `longest` function: `fn longest(x: &str, y: &str) -> &str { ... }`, where two different references are present, and the return reference depends on the logic inside the function, the compiler cannot automatically analyze the lifetimes of references. In such cases, we need to manually specify the relationships between different lifetimes using lifetime annotations.

**Lifetime annotations** do not change the actual duration of any reference. They merely describe the relationships between multiple references, aiding the compiler in its analysis of references but not affecting their lifetimes. Lifetimes use a syntax where the parameter names start with an apostrophe `'`. Its name is very short just like generics, and it is typically all lowercase. The default lifetime `'a` is commonly used. The lifetime annotation is placed after the `&` of a reference and is separated by a space.

- **Metaphor**
    
    Lifetimes in Rust are akin to the life, aging, sickness, and death of values. Lifetime annotations, on the other hand, are like agreements specifying the shared life and death of multiple references. It's similar to the oath taken in the "Oath of the Peach Garden," where the three brothers pledged not to be born on the same day, but to die on the same day. Rust's lifetime annotations serve the purpose of avoiding dangling references, preventing the program from referencing data that should no longer be referenced.
    
- **Use Case**
    
    The lifetimes of the `AccountInfo` structure in solana is as follows. `'a` is a generic lifetimes parameter, indicating that all reference fields of the structure share the same lifetimes. This ensures that the references to the structure are valid within the lifetimes of the structure instance. 
    
    ```rust
    pub struct AccountInfo<'a> {
        pub key: &'a Pubkey,
        pub lamports: Rc<RefCell<&'a mut u64>>,
        pub data: Rc<RefCell<&'a mut [u8]>>,
        pub owner: &'a Pubkey,
        pub rent_epoch: Epoch,
        ……
    }
    ```
    

### Documentation

When multiple references exist in the parameters and return value of a function, manual annotation of lifetimes is required.

```rust
fn longest<'a>(x: &'a str, y: &'a str) -> &'a str {
    if x.len() > y.len() {
        x
    } else {
        y
    }
}
```

In this example, the lifetime annotations for parameters `x` and `y` are both `'a`. The exact duration represented by 'a is not crucial; it simply indicates that the lifetimes of variables `x` and `y` overlap (coexist). The return value is also annotated with 'a, signifying that the lifetime of the return value is the same as the shorter of the lifetimes of `x` and `y`. We will explore specific usage examples in the FAQ.

### FAQ

**Q: How does the `longest` function handle references with different lifetimes?**

A: The following code demonstrates two variables, `string1` and `string2`, each with a different lifetime. The former has a lifetime that extends outside the outer `{}`, while the latter's lifetime is confined to the inner `{}`. Therefore, `'a` represents the lifetime range common to both, which is the shorter of the two, corresponding to the inner `{}`. This ensures that the return value `result` also belongs to the inner `{}`, guaranteeing its validity as long as the lifetimes of `string1` and `string2` intersect. This prevents dangling references, and the code compiles successfully.

```rust
fn main() {
    let string1 = String::from("abcdefghijklmnopqrstuvwxyz");
    {
        let string2 = String::from("123456789");
        let result = longest(string1.as_str(), string2.as_str());
        println!("The longest string is {}", result);
    }
}
```

Next, let's consider another example that reveals that the reference of `result` must have a lifetime shorter than that of both parameters.

```rust
fn main() {
    let string1 = String::from("abcdefghijklmnopqrstuvwxyz");
    let result;
    {
        let string2 = String::from("123456789");
        result = longest(string1.as_str(), string2.as_str());
    }
    println!("The longest string is {}", result);
}
```

In this case, the lifetime `'a` is still the shorter of the two between the variables string1 and string2, that is, the one within the inner {}. However, the lifetime of the return value `result` is now outside the inner `{}`, covering the outer `{}`. This implies that `result` could potentially reference an invalid value, leading to a compilation failure.

> Note: While human observation suggests that the reference of result should be string1, aligning its scope with string1, Rust's compiler adopts a conservative approach. By using lifetime annotations, we inform Rust that the return value of the longest function has a lifetime equal to the shorter of the lifetimes of the input parameters. This is to prevent the possibility of invalid references, even though, theoretically, the code could be valid.
> 

# Example

Next, let's consolidate it and look at the life cycle annotation in the structure definition.

```solidity
// After the structure name + angle brackets to mark the life cycle
struct MyEnum<'a> {
         // Attribute fields use the lifetime marked in the enumeration 'a
         // This means that the lifetime of the greet reference must be greater than the enumeration instance, otherwise an invalid reference will occur
     greet: &'a str,
}

fn main() {
     let hello = String::from("hello, hackquest");
         // The life cycle of the reference is greater than the structure instance, so it can be compiled normally
     let i = MyEnum { greet: &hello };
}
```