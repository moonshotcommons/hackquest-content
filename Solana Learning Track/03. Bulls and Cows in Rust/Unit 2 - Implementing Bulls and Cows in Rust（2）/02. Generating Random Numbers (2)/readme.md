
# Content/**Generating Random Numbers**

After successfully introducing the ***rand*** library in the previous lesson, in this lesson, we will learn how to specifically use the ***rand*** library to generate a random number needed for our game.

### **Writing Code to Generate Random Numbers**

In the `main` function, we will add code to generate a random number between *1* and *100*.

```rust
let secret_number = rand::thread_rng().gen_range(1..101);
```

- ***secret_number***: This will *store* the generated random number.
- ***rand***: This is the library we previously imported, containing functionalities for generating random numbers.
- ***thread_rng***: This is a *function* in the ***rand*** library that returns a random number generator.
- ***gen_range***: This is a *method* of the random number generator used to generate a random number within a specified range. `1..101` defines a range that includes the start value *1* but excludes the end value *101*. Therefore, the actual random number generated will be between *1* and *100* (inclusive of *1* and *100* ).

In short, this line of code declares a variable named ***secret_number*** and calls the **`rand`** library to generate a random integer between *1* and *100* for the current thread's random number generator and assigns it to this variable. This random number will be used in the upcoming game as the **number that players need to guess**.

**Syntax**

Function Call

- hint
    
    ```rust
    std::time::SystemTime::now()
    ```
    
