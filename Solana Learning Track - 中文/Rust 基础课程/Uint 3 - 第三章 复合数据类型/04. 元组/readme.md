# Content/概念

**元组：**是由多种类型元素组合到一起形成的集合，因此它是复合类型，并且它的长度、顺序是固定的。元组通过使用圆括号 `( )` 来定义，其中包含了多个值，各个值之间用逗号 `,` 分隔。

- 比喻
    
    元组，可以想象成购物清单。假设你去超市购物，你的购物清单可以包含不同类型的物品，比如水果、蔬菜和饮料。每个物品就像元组中的一个值，整个购物清单就是一个元组。这个购物清单的长度是固定的，一旦列出了物品，你不能在结账后再随意添加或删除物品。
    
- 真实用例
    
    solana 中提供了一个计算[`program derived address`](https://docs.solana.com/developing/programming-model/calling-between-programs#program-derived-addresses) PDA账户的方法：，该方法的返回值就是元组类型：
    
    ```rust
    // solana_program::pubkey::Pubkey
    
    pub fn find_program_address(
        seeds: &[&[u8]],
        program_id: &Pubkey
    // 返回值为元组，第一个元素为 PDA的公钥地址，第二个为对应的 bump 种子
    ) -> (Pubkey, u8)
    ```
    

### Documentation

元组的创建

```solidity
// 创建1个长度为4，多种不同元素类型的元组
let tup: (i32, f64, u8, &str) = (100, 1.1, 1, "这是一个元组");

// 元组的成员还可以是一个元组
let tup2: (u8, (i16, u32)) = (0, (-1, 1));
```

### FAQ

# Example/示例代码

我们在接下来的代码中演示如何解构、访问元组，以及使用元组作为函数的返回值。

```solidity
fn main() {
    // 创建1个长度为4，多种不同元素类型的元组
    let tup: (i32, f64, u8, &str) = (100, 1.1, 1, "这是一个元组");
    
    // 解构tup变量，将其中第2个元素绑定给变量x
    let (_, x, ..) = tup;
    println!("The value of x is: {}", x);  //1.1

    // 使用.来访问指定索引处的元素
    let first = tup.0;
    let second = tup.1;
    let third = tup.2;
    let fourth = tup.3;
    println!("The value of first is: {}, second is: {}, third is: {}, fourth is: {}", first, second, third, fourth);

    let s = String::from("hello, hackquest.");
    // 函数返回值为元组类型
    let (s1, len) = calculate_length(s);
    println!("The length of '{}' is {}.", s1, len);
}

// len() 返回字符串的长度
fn calculate_length(s: String) -> (String, usize) {
    let length = s.len();

    (s, length)
}
```