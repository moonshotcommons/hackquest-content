# Content/Define getTokensByOwner Function

We have just defined an ***ownerTokens*** *mapping* for the query *function* and updated the ***mint** function*, now, everything is ready.

Now, we will create a *function* to help us query all NFTs owned by a specified address. This *function* provides a simple way to keep track of the NFTs you own.

Since we mentioned earlier that this *function* is for querying, we need an input *parameter* to indicate the account *address* to be queried.

The return value of the query should be an array of `uint256` type, representing all TokenIds owned by that *address*.

It should be `view` and `public` because we don’t modify any *states* in query *functions* and we’d like it to be available for anyone to query.

**Syntax**

function parameters, return, calling, data location, address

- hint
    
    ```solidity
    function getTokens(address _owner) public view returns (uint256[] memory) { }
    ```
    
