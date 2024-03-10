# Content/**定义Token结构体**

首先需要一个数据结构来存储NFT的详细信息，例如名字，描述，持有者，而**结构体**是所有数据结构中最合适的。

**Syntax**

struct

- 提示
    
    ```solidity
    contract Example{
    		// 定义 A 结构体，用于存储 Apple 的信息
        struct A {
            string name;        //A 名称
            string description; //A 描述信息
            address owner;      //A 所有者地址
        } 
    }
    ```