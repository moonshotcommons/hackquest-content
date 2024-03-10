# Content

**Control Flow** is a crucial part of writing programs as it determines the program's execution flow. Rust's syntax for control flow is concise yet powerful, offering essential tools for building program logic. Common control flow statements in Rust include `if expressions`, `for loops`, `while loops`, and `loop loops`. Proper use of these constructs can make programs clearer and more efficient.

- **Metaphor**
- **Use Case**
    
    Let's take an example from Solana regarding movie reviews. When a user adds a movie review, a series of security checks are performed. If the checks pass, the program continues execution; otherwise, an exception is thrown, and the process is interrupted.
    
    ```rust
    // Add a movie review
    pub fn add_movie_review(
        program_id: &Pubkey,
        accounts: &[AccountInfo],
        title: String,
        rating: u8,
        description: String
    ) -> ProgramResult {
    
        // Check data validity first; if the rating is not in the range 1~5, throw an error and interrupt the process
        if rating > 5 || rating < 1 {
            msg!("Rating cannot be higher than 5");
            return Err(ReviewError::InvalidRating.into())
        }
    
        // Continue the process, do something
    
        // If not a signature user, throw an error and interrupt the process
        if !initializer.is_signer {
            msg!("Missing required signature");
            return Err(ProgramError::MissingRequiredSignature)
        }
    
        // Continue the process, do something
    
        // If not a PDA account, throw an error and interrupt the process
        if pda != *pda_account.key {
            msg!("Invalid seeds for PDA");
            return Err(ReviewError::InvalidPDA.into());
        }
    
        // Continue the process, do something
    
        // If the space usage exceeds 1000 bytes, throw an error and interrupt the process
        if total_len > 1000 {
            msg!("Data length is larger than 1000 bytes");
            return Err(ReviewError::InvalidDataLength.into())
        }
    
        // Complete the process, end
        Ok(())
    }
    ```
    

### Documentation

The following code demonstrates four common control flow commands in Rust, covering most scenarios in the programming process:

```solidity
fn main() {
    let condition = true;
    // if else syntax
    if condition {
        // do something
    } else {
        // do something else
    }

    // for loop
    for i in 1..=5 {
        println!("{}", i);
    }

    // while loop
    let mut m = 1;
    while m <= 5  {
        println!("{}!", m);
        m = m + 1;
    }

    // loop loop
    let mut n = 1;
    loop {
        println!("{}!!", n);
        n = n + 1;
        if n > 5 {
            break;
        }
    }
}
```

### FAQ

# Example

Here are the specific usage scenarios of `if`, `for`, `while`, and `loop` to help you better understand their usage. It should be noted that both if and loop can be used as expressions, and assignment operations can be performed through return values.

```solidity
fn main() {
     let condition = true;
     // 1. If branch assignment, the if statement block is an expression, and the return value of the if expression can be used to assign a value to the variable.
     let number = if condition {
         5
     } else {
         6
     };
     println!("The value of number is: {}", number); // print 5

     // 2. Loop skipping and interruption
     for item in 1..=5 {
         if item == 2 {
             // Skip this loop and enter the next loop
             continue;
         }

         if item == 4 {
             // Break the entire loop
             break;
         }
         println!("this Item is : {}", item);
     }

     // 3. Ownership transfer occurs in For loop
     let vec1: Vec<i32> = vec![1, 2, 3, 4, 5];
     for item in vec1.into_iter() {
         println!("Item: {}", item);
         // Any operation can be done on the item here because ownership has been moved to the loop
     }
     // Printing the vec1 variable here fails because ownership has been transferred to the for loop
     // println!("{:?}", vec1)

     // 4. For loop borrows collection elements: immutable borrowing
     let vec2: Vec<i32> = vec![1, 2, 3, 4, 5];
     // Ownership borrowing occurs via &vec2
     for item in &vec2 {
         println!("Item: {}!", item);
     }
     //Here vec2 still has ownership
     println!("{:?}", vec2);

     // 5. while vs for loop
     let a: [i32; 5] = [10, 20, 30, 40, 50];
     let mut index = 0;
     // Accessing elements by specifying indexes in the while loop may cause the risk of crossing the boundary.
     while index < 5 {
         println!("the value is: {}", a[index]);
         index = index + 1;
     }

     // In the for loop, the elements are traversed through the iterator and the index is not used to access the array, so there is no risk of crossing the boundary.
     // At the same time, it also avoids boundary checking at runtime and has higher performance.
     for element in a.iter() {
         println!("the value is: {} !", element);
     }

     // 6. Loop loop as expression
     let mut counter = 0;
     let result = loop {
         counter += 1;
         if counter == 10 {
             // When the condition is met, break will interrupt the loop and return the value of counter * 2
             break counter * 2
         }
     };
     println!("The result is {}", result);
}
```