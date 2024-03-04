# Content/概念

`Hashmap` ****是 Rust 语言中的一个集合类型，用于存储键与值（key-value）的对应关系。每个键`key`映射到一个值`value`，键必须是唯一的。这种结构允许我们通过键快速检索到值，而不需要遍历整个集合。Hashmap 的高效性来自于它的散列函数，这个函数能够将键转换成存储位置的索引，从而直接访问内存中的位置，这样就大大加快了查找速度。

- 比喻
    
    HashMap 这种数据结构类似于现实中的图书馆：每本书（值）都有一个唯一的索书号（键），图书管理员可以通过索书号在图书馆的电脑系统（Hashmap）中迅速找到书的具体位置。这比起逐个书架查找要快得多，因为系统内部使用索书号直接定位到书的位置，就像 Hashmap 使用键直接定位到值。
    
- 真实用例
    
    不仅在HashMap中使用哈希函数，在区块链领域哈希函数更是一个重要的存在，solana 的账户地址，就是通过将账户的公钥进行 SHA-256 和 Keccak（SHA-3）哈希得到的，并最终用Base58编码（去除了Base64中比较容易混淆的字符，如0、o、1、l等）。
    

### Documentation

可以使用如下2种方式创建 HashMap，如果预先知道要存储的 key-value 对个数，可以创建指定大小的 HashMap，避免频繁的内存分配和拷贝，提升性能。

```solidity
// 由于 HashMap 并没有包含在 Rust 的 prelude 库中，所以需要手动引入
use std::collections::HashMap;
fn main() {
    // 创建一个HashMap，用于存储学生成绩
    let mut student_grades = HashMap::new();
    student_grades.insert("Alice", 100);
    
    // 创建指定大小的 HashMap，避免频繁的内存分配和拷贝，提升性能。
    let mut student_grades2 = HashMap::with_capacity(3);
    student_grades2.insert("Alice", 100);
    student_grades2.insert("Bob", 99);
    student_grades2.insert("Eve", 59);
}
```

### FAQ

# Example/示例代码

通过如下的示例我们来学习数组如何转成 HashMap，以及 HashMap的查询、遍历、更改等操作。

```solidity
use std::collections::HashMap;
fn main() {
    // 动态数组，类型为元组 (用户，余额)
    let user_list: Vec<(&str, i32)> = vec![
        ("Alice", 10000),
        ("Bob", 1000),
        ("Eve", 100),
        ("Mallory", 10),
    ];

    // 使用迭代器和 collect 方法把数组转为 HashMap
    let mut user_map: HashMap<&str, i32> = user_list.into_iter().collect();
    println!("{:?}", user_map);

    // 通过 hashmap[key] 获取对应的value
    let alice_balance = user_map["Alice"];
    println!("{:?}", alice_balance);

    // 通过 hashmap.get(key) 获取对应的value，返回值为 Option 枚举类型
    let alice_balance: Option<&i32> = user_map.get("Alice");
    println!("{:?}", alice_balance);

    // 不存在的key，返回值为 None，但不会报错
    let trent_balance: Option<&i32> = user_map.get("Trent");
    println!("{:?}", trent_balance);

    // 覆盖已有的值，insert 操作 返回旧值
    let old = user_map.insert("Alice", 20000);
    assert_eq!(old, Some(10000));

    // or_insert 如果存在则返回旧值的引用；如果不存在，则插入默认值，并返回其引用
    let v = user_map.entry("Trent").or_insert(1);
    assert_eq!(*v, 1); // 不存在，插入1

    // 验证Trent对应的值
    let v = user_map.entry("Trent").or_insert(2);
    assert_eq!(*v, 1); // 已经存在，因此2没有插入
}
```