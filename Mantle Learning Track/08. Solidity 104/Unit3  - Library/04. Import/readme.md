# Content/Content

### Concept

Great! After learning about library, in this section, we’ll learn an essential syntax in Solidity, which is the `import` statement. The `import` keyword in Solidity enables the use of *functions* or code from external *contracts* or *libraries*, essentially copying the code from another `.sol` file into the current one.

- Metaphor
    
    Just like preparing a complex dish, you need a variety of different ingredients and seasonings. In this example, the contract is like the dish, and the `import` statement tells people where to find the relevant ingredients and seasonings.
    
- Real Use Case
    
    In [ERC20](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/ERC20.sol), you can see the use of import.
    
    ```solidity
    import {IERC20} from "./IERC20.sol";
    import {IERC20Metadata} from "./extensions/IERC20Metadata.sol";
    import {Context} from "../../utils/Context.sol";
    import {IERC20Errors} from "../../interfaces/draft-IERC6093.sol";
    ```
    

### Documentation

You can use the `import` keyword followed by the file path (both relative and absolute paths are acceptable) to import a specific contract file.

```solidity
import "./SafeMath.sol";
```

### FAQ

- Can I import only specific functions or structs from another Solidity file, and if so, how do I do that?
    
    Yes, you can import specific *functions*, *structs*, or even *contracts* from another Solidity file. To do so, you specify what you want to import using curly braces `{}` after the `import` keyword and the file path. For example:
    
    ```solidity
    //This will only import SomeStruct and someFunction from AnotherContract.sol
    import { SomeStruct, someFunction } from "./AnotherContract.sol";
    ```
    
- What is the syntax for importing another Solidity file into my current contract file?
    
    In Solidity, you can import another file using the `import` keyword followed by the path to the file you want to import. The path can be relative or absolute. 
    
    ```solidity
    // basic example
    import "./AnotherContract.sol";
    
    // If you're using a package manager like npm and installed a Solidity package
    import "@openzeppelin/contracts/token/ERC20/IERC20.sol";
    ```
    

# Example/Example

```solidity
// OtherContract.sol
pragma solidity ^0.8.0;

contract OtherContract {
  uint256 public someVariable;

  constructor(uint256 _initialValue) {
    someVariable = _initialValue;
  }

  function someFunction() external view returns (uint256) {
    return someVariable;
  }
}
```

```solidity
pragma solidity ^0.8.0;

// import other contract
import "./OtherContract.sol";

contract ExampleContract {
  // use the contract we imported
  OtherContract public otherContract;

  // constructor
  constructor(address _otherContractAddress) {
    // create instances of other contracts
    otherContract = OtherContract(_otherContractAddress);
  }

  // call functions of other contracts
  function callOtherContractFunction() external view returns (uint256) {
    // use imported contract instances to call functions
    return otherContract.someFunction();
  }
}
```
