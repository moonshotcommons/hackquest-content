# Content/Query information of kitty’s mom and dad

After defining the function, we need to retrieve the basic information of both the mom and dad kitties. This information is stored in the ***kitties*** *mapping*.

We can directly access the ***Kitty*** *struct* associated with the given ***momId*** and ***dadId***, from the ***kitties** mapping*.

In Solidity, when working with *structs*, we must specify the storage location. Since we don't intend to modify the information of the mom and dad kitties, we'll store them in `memory`. This approach will help in saving a significant amount of *gas*.

**Syntax**

mapping

- hint
    
    ```solidity
    //For example, here we gain the Student struct stored in the students mapping corresponding to the studentId
    Student memory a = students[studentId];
    ```
    
