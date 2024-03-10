# Content/**定义一个存储某个NFT的TokenId所对应的NFT属性的映射**

有了***Token***这个结构体后，一般而言，我们都需要一个**映射**来存储它，在这里，我需要把***tokenId***和***Token***对应起来，所以需要创建一个从*uint256⇒Token*的映射。

**Syntax**

mapping

- 提示
    ```
    contract Example{
		// 定义 Apple 结构体，用于存储 Apple 的信息
    struct A {
        string name;        // A 名称
        string description; // A 描述信息
        address owner;      // A 所有者地址
        }
    
    mapping(uint256 => A) private apples;
    }
    ```