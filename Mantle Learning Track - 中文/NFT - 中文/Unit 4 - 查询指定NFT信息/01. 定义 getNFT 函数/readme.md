# Content/**定义 getNFT 函数**

首先，让我们明确该函数的作用。我们之前提到，该*函数*用于查询特定 NFT 的相关信息。因此，我们需要一个入参来指定要查询的 NFT 的TokenId。

为了确保查询*函数*不会修改*合约*的状态变量，我们应将其修饰为view。

在选择*函数*的*可见性*时，我们选择使用 public，这样无论是在*合约内部*还是在*合约外部*，都可以访问该*函数*来查询 NFT 的信息。

作为查询*函数*，最重要的是定义返回值。为了方便演示，我们选择将 NFT 的 ***name***、***description*** 和 ***owner*** 逐一返回，并且使用了已命名的*返回值*。

由于string类型的*变量*在作为*局部变量*时必须指定数据的**存储位置**，而我们没有将它存储在storage的需求，所以我们将其定义为memory。

**Syntax**

return,data location

- 提示
    ```
    //定义了一个getNFT函数
    function getNFT(uint256 _tokenId) public view returns (string memory name, string memory description, address owner){

    }
    ```