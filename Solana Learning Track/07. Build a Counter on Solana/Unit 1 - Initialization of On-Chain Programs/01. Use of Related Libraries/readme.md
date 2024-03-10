# Content/Use of related libraries

Now, let's start writing our code! The first is to import the related libraries.

### Using the Anchor framework

In order to take full advantage of the powerful capabilities of the *Anchor*, we first introduce ***anchor_lang***. It provides us with the core functionality and type definitions of the Anchor.

### Using the DerefMut attribute

In order to allow us to modify complex data structures more naturally, we need to introduce ***DerefMut*** from the Rust standard library. This feature makes manipulating encapsulated data as easy as using ordinary variables, thus simplifying code and improving readability.
For example, when we need to process account data later, ***DerefMut*** can make obtaining and modifying data from the account status more direct and concise.

**Syntax**

use

- hint
    
    ```rust
    use anchor_lang::prelude::*;
    use std::ops::DerefMut;
    ```