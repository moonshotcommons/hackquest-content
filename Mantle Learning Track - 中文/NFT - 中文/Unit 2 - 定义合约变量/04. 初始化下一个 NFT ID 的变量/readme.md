# Content/初始化下一个 NFT ID 的变量

同时我们还需要一个指针来指向下一个要铸造的NFT，所以我们需要定义一个 整型 变量。

**Syntax**

uint256

- 提示
    ```
    contract Example{
		// 定义 Apple 结构体，用于存储 Apple 的信息
    struct A {
        string name;        // A 名称
        string description; // A 描述信息
        address owner;      // A 所有者地址
        }
    
    mapping (uint256 => A) private a;

		mapping(address => uint256[]) private ownerTokens;
		
		uint256 nextTokenId = 1;
    }
    ```
