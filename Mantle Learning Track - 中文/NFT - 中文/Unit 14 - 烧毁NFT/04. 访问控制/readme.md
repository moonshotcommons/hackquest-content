# Content/**访问控制**

我们在定义函数时提到过，该*函数*需要做访问控制，限制调用者必须是NFT的拥有者。

现在，我们获取到了NFT的信息，那么其拥有者我们也就知道了。现在就可以来做访问控制了！

**Syntax** 

variable

- 提示
    
    ```solidity
    require(owner != msg.sender, "error");
    ```