# Content/Content

When writing a *contract*, in some cases, specific *functions* in the *contract* will be called by other *contracts*, and the *functions* are shared with other contracts. In this case, we can use the `external` keyword

- Metaphor
    - `external` is like a public library, accessible to all, but only during opening hours. Anyone can read, but they cannot conduct private activities in the library. (Only `external` functions can be used).
- Real Use Case
    
    In OpenZepplin's ***GovernorTimelockControl*** contract, an ***[updateTimelock](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/9ef69c03d13230aeff24d91cb54c9d24c4de7c8b/contracts/governance/extensions/GovernorTimelockControl.sol#L145C14-L145C28)*** function is defined for use by external users or contracts.
    
    ```solidity
    function updateTimelock(TimelockController newTimelock) external virtual onlyGovernance {
            _updateTimelock(newTimelock);
    }
    ```
    

### Documentation

To define a *function* that can be used by external users or other contracts, we use the keyword `external` and place it after the *function parameters*.

<aside>
💡 `this` keyword must be added when used in this *contract*.

</aside>

```solidity

   function aa() internal{}

   this.aa();
```

### **FAQ**

- Can state variables be defined by `external`?
    
    `external` cannot be used to define variables.
    
- Are there any special requirements for function visibility of interface contracts?
    
    All *functions* in the interface must be `external`.
    

# Example/Example

```solidity
contract A {

    uint public result;

    function aa(uint a) external {
        result = a + 1;
    }

    function b(uint b) public {
         this.aa(b);
    }
}
```
