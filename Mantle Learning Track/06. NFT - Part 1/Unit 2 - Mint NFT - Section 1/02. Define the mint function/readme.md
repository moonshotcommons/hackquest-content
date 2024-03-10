# Content/Define the mint function.

Let's define the ***mint** function*.

In order to **create the NFT**, you need some information: the name, description of the specified NFT, and the owner. 

However, not everything is the input parameter. Since the owner is the caller of this *function*, we don’t need to have an owner as the *parameter*, but other two pieces of information, we need it from the caller.

To obtain the TokenId of the newly created NFT, the *function* needs to return a uint256 value.

**Syntax**

function parameters, return, calling, string, data location

- hint
    
    ```solidity
    //Here is the standard definition of mint
    // Please note that variable-length types such as string must specify their storage location when used as input parameters
    // Here, we only need to read the parameter content, so we use memory.
    function mint(string memory _name, string memory _description) public {}
    ```
    