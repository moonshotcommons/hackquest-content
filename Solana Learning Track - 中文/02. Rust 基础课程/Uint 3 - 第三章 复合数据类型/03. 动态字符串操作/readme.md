# Content/概念

前面我们已经对字符串有了一定的了解，接下来我们继续学习字符串相关的操作：追加、插入、替换、删除等。

- 比喻
    
    字符串就像由一节节车厢组成的火车，我们可以对火车各种操作，比如要提高运力，那需要把两列火车车厢拼接在一起；如果某节车厢坏了，我们可以把它拆下来，修好后再插入或者直接挂载到火车尾。
    
- 真实用例

### Documentation

**字符串**是由**字符**组成的连续集合，Rust 中字符采用 Unicode 字符集，约定每个字符4个字节，但在实际的编码中，Rust 对字符串采用 UTF-8 编码，也就是每个字符所占的字节数是变化的(1 - 4)。这样有助于大幅降低字符串所占用的内存空间。

```solidity
let say = String::from("hello,世界");
// 长度为12
// utf-8对ascii字符用1个字节，对常见汉字采用3个字节编码
println!("长度为:{}", say.len());
```

### FAQ

- Q：字节、字符、字符串这几个概念有区别？
    
    A：**字节**（byte）是一个长度单位，跟使用哪种编程语言没有关系，在计算机中它占据8个bit位，类似于`0111 1010`这样。**字符**（Character）是一种文本数据类型，表示文本中的一个单个字符，Rust 采用 `char` 表示为字符类型 。**字符串**是由字符组成的序列，Rust 中字符串类型是 `String`。
    

# Example/示例代码

接下来我们介绍下字符串的追加 (Push)、插入 (Insert)、替换 (Replace)、删除 (Delete)操作。

```solidity
fn main() {
    let mut s = String::from("Hello ");

    // 追加字符串，修改原来的字符串，不是生成新的字符串
    s.push_str("rust");
    println!("追加字符串 push_str() -> {}", s);

    // 追加字符
    s.push('!');
    println!("追加字符 push() -> {}", s);

    // 插入字符，修改原来的字符串，需要指定索引位置，索引从0开始，
    // 如果越界则会发生错误
    s.insert(5, ',');
    println!("插入字符 insert() -> {}", s);

    // 插入字符串
    s.insert_str(6, " I like");
    println!("插入字符串 insert_str() -> {}", s);

    // replace 替换操作生成新的字符串。需要2个参数，第一个参数是
    // 要被替换的字符串，第二个参数是新的字符串
    let str_old = String::from("I like rust, rust, rust!");
    let str_new = str_old.replace("rust", "RUST");
    println!("原字符串长度为:{},内存地址:{:p}", str_old, &str_old);
    println!("新字符串长度为:{},内存地址:{:p}", str_new, &str_new);

    // pop 删除操作，修改原来的字符串，相当于弹出字符数组的最后一个字符
    // 返回值是删除的字符，Option类型，如果字符串为空，则返回None
    // 注意：pop是按照“字符”维度进行的，而不是“字节”
    let mut string_pop = String::from("删除操作，rust 中文!");
    // 此时删除的是末尾的感叹号“！”
    let p1 = string_pop.pop();
    println!("p1:{:?}", p1);
    // 在p1基础上删除末尾的“文”
    let p2 = string_pop.pop();
    println!("p2:{:?}", p2);
    // 此时剩余的字符串为“删除操作，rust 中”
    println!("string_pop:{:?}", string_pop);
}
```