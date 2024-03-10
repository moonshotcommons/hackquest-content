# Content/Calculate the generation number

After calculating the kitty's gene, we also need to calculate its generation number.

The generation number of the kitty is equal to the max generation number of the *dad* and *mom*, **plus one**.

> For example:
> 
> 
> 0th generation dad x 0th generation mom = 1st generation kitty
> 
> 1st generation dad x 1st generation mom = 2nd generation kitty
> 
> 1st generation dad x 0th generation mom = 2nd generation kitty
> 

We can accomplish this series of operations in a single expression using the **ternary operator**.

**Syntax**

ternary operator

- hint
    
    ```solidity
    //In this example, if a is greater than b, then num is 0, and if a is less than b, then num is 1.
    uint256 num = 1 > 2 ? 0 : 1;
    ```
    
