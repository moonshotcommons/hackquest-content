# Content/概念

**字符类型**是用`char`类型表示的，占用`4`个字节的空间，可以表示Unicode字符集中的任何字符，包括ASCII字符、各种符号、各种语言的文字，甚至是表情符号。通过单引号`'`可以创建一个char类型的值。例如`let a:char = '🦀';`

**布尔类型**有两种值：`true` 和 `false`，占用内存的大小为 `1` 个字节。

注意：这里是介绍的是字符（用单引号`''`表示)，不是字符串(用双引号`""`表示)，字符串涉及的内容比较多，我们放在后面来讲。

- 扩展
    
    这里我们稍微扩展下字符类型的背景知识：计算机处理的所有内容，在底层都是数字，包括我们写下的各种可见字符以及不可见字符，在计算机里都有一个数字跟它对应，计算机只处理这个数字，而人们需要定义好这个数字代表的是什么字符（比如数字`97`代表字符`a`）。在1960年的时候，美国制定了`ASCII`字符编码标准，它只包含了128个字符（英文大小写字母、数字、标点符号，以及一些非打印字符如回车、换行、制表符等），那个年代128个够用了。后来随着计算机的普及，世界各国人民都要使用计算机，当然不可能都用英文。于是，一种可以容纳所有语言的字符编码系统`Unicode`应运而生，也就是世界上任何一种语言的单个字母、汉字、日文、韩文等，都在Unicode字符集里有个数字跟它一一对应，它可以表示的字符超过110,000个。
    当然，Unicode字符集只是一种字符和数字的映射关系，它是一种抽象的定义，真正使用过程中（比如显示、打印文字）这个数字怎么存储和传输，就涉及到了编码方式，常见的有`GBK`、`UTF-8`、`UTF-16`等等。其中，GBK 采用固定的**双字节**编码，即每个字符占用 2 个字节。而 UTF-8 是一种**变长编码**，可以使用 1 到 4 个字节来表示一个字符。对于 ASCII 字符，UTF-8 只需要 1 个字节，而其他字符可能需要 2、3 或 4 个字节，由于它的灵活性，所以很多场景下UTF-8更受欢迎。
    
- 真实用例
    
    solana 的账户`AccountInfo`结构体中，通过`bool`类型标识该账户是否有对应属性。它的账户体系分为**程序账户**和**数据账户**，前者只有程序（智能合约），负责执行逻辑，后者只负责存储数据（状态），这跟以太坊的智能合约即包含程序又包含状态有很大不同。
    
    ```rust
    // solana_program::account_info::AccountInfo
    
    pub struct AccountInfo {
        // ……
    
    		// 是否可写，为 True 则为数据账户，负责存储数据
        pub is_writable: bool,
    		// 是否可执行，为 True 则为程序账户，负责执行逻辑
        pub executable: bool,
    }
    ```
    

### Documentation

```solidity
// 英文字符
let c = 'z';
// 数学符号
let z = 'ℤ';
// 中文字符
let g = '国';
// emoji表情
let ferris = '🦀';

// 布尔类型
let m = true;
```

### FAQ

- Q：布尔类型在进行逻辑运算时的**短路原则**是什么？
    
    A：对于`& 与`运算`（a & b）`，如果第`a`为`false`，那么程序就不用再去计算判断变量b的值，因为不管b是什么值，结果都是fasle，这就是短路原则。同样，对于`| 或`运算`（a | b）`，如果a为`true`，那么程序就不用再去计算判断变量b的值，这同样是短路原则。所以，在进行`& 与`、`|或`运算时，我们一般要把计算量小的表达式放在前面，这样就更容易命中短路原则，避免程序先进行复杂的表达式计算，从而影响到程序效率。
    

# Example/示例代码

使用`char`类型打印各国字符，并测测`'你'`和`'我'`中间有多少个字符。

```solidity
use std::thread;
use std::time::Duration;

// 这个函数耗时3秒
fn get_calculate_result() -> bool {
		// 模拟复杂计算，耗时3s
		thread::sleep(Duration::from_secs(3));
    println!("called this function");
    false
}

fn main() {
    // 打印各国语言的单个字符
    let thai_char  = 'ก';
    let korean_char = '한';
    let traditional_chinese_char = '繁';
    let indonesian_char = 'ä';
    // 注意，这里str是字符串类型，不是字符，只不过长度为1
    let str = "国";
    println!("thai_char : {}", thai_char );
    println!("Korean: {}", korean_char);
    println!("Traditional Chinese: {}", traditional_chinese_char);
    println!("Indonesian: {}", indonesian_char);
    
    //测测你和我中间有多少个字符
    for i in '你'..='我' {
        print!("{}", i);//你佡佢佣……戏成我，中间共有4786个字符
    }
    
    let f: bool = true;
    // 触发短路原则，不会调用get_calculate_result函数进行复杂计算
    // 如果改成 get_calculate_result() | f，则会先调用函数，有性能影响
    if f | get_calculate_result() {
        println!("Success!");
    }    
} 
```