# Content/**完善mint函数**

非常好！到现在为止，你已经完成了**mint功能**的所有逻辑。

但在最后，我们还需要将铸造的NFT的tokenId返回给调用者，让他知道它铸造的NFT是哪一个。

需要注意的是我们要返回的这个tokenId应该是此次铸造的NFT所对应的Id，因此我们应该return的值是nextTokenId-1。

> 这是由于刚刚进行了nextTokenId++;
另一种更好的做法是在nextTokenId++之前使用局部变量将铸造的tokenId预先存储起来。
> 

**Syntax**

variable,function return

- 提示
    ```
    return 1;
    ```