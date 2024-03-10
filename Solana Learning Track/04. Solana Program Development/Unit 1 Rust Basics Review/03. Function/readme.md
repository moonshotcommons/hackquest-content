# Content

Learning Objectives: In this section, we will complete the definition of a Rust function.

### Define Function Name

In Rust, we use the `fn` keyword to define a function, followed by the function name and a set of parentheses.

```rust
fn process_instruction()
```

Next, we can add parameters to the function by introducing variable names and their corresponding data types.

### Define Function Parameters

Rust is known as a "statically-typed" language, where every value in Rust has some kind of "data type." This means Rust needs to know the type of every variable at compile time. In cases where there could be multiple types, we must add type annotations to the variables.

In the example below, we create a function named `process_instruction` that takes the following parameters:

- `program_id` of type `&Pubkey`
- `accounts` of type `&[AccountInfo]`, meaning it is a reference to an array of AccountInfo structs.
- `instruction_data` of type `&[u8]`, meaning it is a reference to an array of u8 types.

Note the `&` before the type of each parameter in the `process_instruction` function. In Rust, `&` signifies a **reference** to another variable. This allows you to reference a value without taking ownership of it. "References" ensure a valid value of a specific type is pointed to. The action of creating references in Rust is called **borrowing**.

In this example, when calling the `process_instruction` function, the user must pass values for the required parameters. Then, the `process_instruction` function references the values passed by the user, ensuring each value is of the correct data type specified in the `process_instruction` function.

Additionally, note the square brackets `[]` around `&[AccountInfo]` and `&[u8]`. This means that the `accounts` and `instruction_data` parameters represent **slices** of AccountInfo and u8 types, respectively. "Slices" are similar to arrays (collections of objects of the same type) but with an unknown length at compile time. In other words, the `accounts` and `instruction_data` parameters are inputs of unknown length.

```rust
fn process_instruction(
    program_id: &Pubkey,
    accounts: &[AccountInfo],
    instruction_data: &[u8],
)

```

### Define Function Return Value

Next, we can make the function return a value by declaring the return type using an arrow `->`.

In the example below, the `process_instruction` function now returns a value of type `ProgramResult`. We will discuss this further in the next section.

```rust
fn process_instruction(
    program_id: &Pubkey,
    accounts: &[AccountInfo],
    instruction_data: &[u8],
) -> ProgramResult {
    // do something...
}
```